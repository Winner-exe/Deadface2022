<h1>Counting Heads</h1>

<h2>Problem</h2>
DEADFACE compromised a database from Eastern State University. They fired their security team, and now they're reaching out to you to see if you can help them figure out the scope of the breach. Below is a link to the compromised database.

How many users are in the database? Submit the flag as flag{#}.

Download File
SHA1: 371f9bcc71efa6b0a280546943be13fea705c8c0
Password: d34df4c3
<h2>Solution</h2>
After spending an aggregious amount of time getting MariaDB to work on my device, I ran the following queries to load the <code>esu.sql</code> file.

```
mysql -u root -p
CREATE esu;
exit

mysql -u root -p esu < esu.sql
USE esu;
```

I then ran the query `SHOW TABLES;` to see the different tables in the sql dump:
```
+------------------+
| Tables_in_esu    |
+------------------+
| countries        |
| courses          |
| degree_types     |
| enrollments      |
| passwords        |
| payment_statuses |
| programs         |
| roles            |
| roles_assigned   |
| states           |
| term_courses     |
| terms            |
| users            |
+------------------+
13 rows in set (0.000 sec)
```

Then to find out the structure of the `users` table, I ran `DESC users;` to get:
```
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| user_id  | int(11)     | NO   | PRI | NULL    | auto_increment |
| username | varchar(52) | NO   | UNI | NULL    |                |
| first    | varchar(52) | NO   |     | NULL    |                |
| last     | varchar(52) | NO   |     | NULL    |                |
| middle   | varchar(24) | YES  |     | NULL    |                |
| email    | varchar(52) | NO   | UNI | NULL    |                |
| street   | varchar(52) | NO   |     | NULL    |                |
| city     | varchar(52) | NO   |     | NULL    |                |
| state_id | int(11)     | NO   | MUL | NULL    |                |
| zip      | varchar(10) | NO   |     | NULL    |                |
| gender   | varchar(8)  | NO   |     | NULL    |                |
| dob      | date        | NO   |     | NULL    |                |
+----------+-------------+------+-----+---------+----------------+
12 rows in set (0.001 sec)
```

I then ran `SELECT COUNT(user_id) FROM users;` to get the count of 2400:
```
+----------------+
| COUNT(user_id) |
+----------------+
|           2400 |
+----------------+
1 row in set (0.001 sec)
```

`flag{2400}`

<h1>The Faculty</h1>

<h2>Problem</h2>
How many of the compromised users in the database are not students?

Submit the flag as flag{#}.

Use the database from Counting Heads.

<h2>Solution</h2>
Since this question deals with the roles, I tried running `DESC roles;` to get:

```
+-----------+-------------+------+-----+---------+----------------+
| Field     | Type        | Null | Key | Default | Extra          |
+-----------+-------------+------+-----+---------+----------------+
| role_id   | int(11)     | NO   | PRI | NULL    | auto_increment |
| role_name | varchar(56) | NO   | UNI | NULL    |                |
+-----------+-------------+------+-----+---------+----------------+
2 rows in set (0.001 sec)
```

It looked like this table just showed which `role` corresponds with wich `role_id`, so to see the mapping, I ran `SHOW * FROM roles;`:
```
+---------+---------------------+
| role_id | role_name           |
+---------+---------------------+
|       5 | Adjunct Professor   |
|       8 | Administration      |
|       4 | Associate Professor |
|       2 | Instructor          |
|       3 | Professor           |
|       6 | Research Assistant  |
|       7 | Research Associate  |
|       1 | Student             |
+---------+---------------------+
8 rows in set (0.001 sec)
```

Now I knew that the Student `role_id` was 1.

I moved to the `roles_assigned` table to see which users were assigned to which roles.
```
MariaDB [esu]> DESC roles_assigned;
+------------------+---------+------+-----+---------+----------------+
| Field            | Type    | Null | Key | Default | Extra          |
+------------------+---------+------+-----+---------+----------------+
| role_assigned_id | int(11) | NO   | PRI | NULL    | auto_increment |
| user_id          | int(11) | NO   | MUL | NULL    |                |
| role_id          | int(11) | NO   | MUL | NULL    |                |
+------------------+---------+------+-----+---------+----------------+
3 rows in set (0.001 sec)
```

Finally, I ran `SELECT COUNT(user_id) FROM roles_assigned WHERE NOT role_id=1;` to get the answer of 627:
```
+----------------+
| COUNT(user_id) |
+----------------+
|            627 |
+----------------+
1 row in set (0.001 sec)
```
<h1>Let's Hash It Out</h1>

<h2>Problem</h2>
DEADFACE discussed what users they were going to target out of the database dump obtained. Look around on Ghost Town and submit the password hash of the user they are targeting.

Submit the flag as flag{hash}.

Use the database from Counting Heads.

<h2>Solution</h2>
Looking at this <a href="https://ghosttown.deadface.io/t/database-question/46/5">GhostTown thread,</a> it looks like Deadface planned to target Administration, which is a role assigned to only one person. From the work done in "Counting Heads," I knew that the `role_id` for Administration was 8.

With this in mind, I ran the query `SELECT user_id FROM roles_assigned WHERE role_id=8;` to get:
```
+---------+
| user_id |
+---------+
|    1440 |
+---------+
1 row in set (0.000 sec)
```

Now to get this user's password, I first ran `DESC passwords;` to understand the structure of the password database:
```
+-------------+--------------+------+-----+---------+----------------+
| Field       | Type         | Null | Key | Default | Extra          |
+-------------+--------------+------+-----+---------+----------------+
| password_id | int(11)      | NO   | PRI | NULL    | auto_increment |
| password    | varchar(256) | NO   | UNI | NULL    |                |
| user_id     | int(11)      | NO   | UNI | NULL    |                |
+-------------+--------------+------+-----+---------+----------------+
3 rows in set (0.001 sec)
```

Since `user_id` was one of the columns, I just ran `SELECT password FROM passwords WHERE user_id=1440;` to get:
```
+------------------------------------------+
| password                                 |
+------------------------------------------+
| b487af41779cffb9572b982e1a0bf83f0eafbe05 |
+------------------------------------------+
1 row in set (0.000 sec)
```

This means the user's password hash is `b487af41779cffb9572b982e1a0bf83f0eafbe05`.

`flag{b487af41779cffb9572b982e1a0bf83f0eafbe05}`

<h1>Fall Classes</h1>

<h2>Problem</h2>
How many unique Fall courses are present in the database dump? Submit the flag as flag{#}.

Use the database from Counting Heads.

<h2>Solution</h2>

I first got some information about the structure of the `courses`, `term_courses`, and `terms` tables:
```
MariaDB [esu]> DESC courses;
+------------------+---------------+------+-----+---------+----------------+
| Field            | Type          | Null | Key | Default | Extra          |
+------------------+---------------+------+-----+---------+----------------+
| course_id        | int(11)       | NO   | PRI | NULL    | auto_increment |
| title            | varchar(128)  | NO   |     | NULL    |                |
| level            | varchar(32)   | NO   |     | NULL    |                |
| description      | varchar(128)  | NO   | UNI | NULL    |                |
| long_description | varchar(1024) | YES  |     | NULL    |                |
| sem_hours        | int(11)       | NO   |     | NULL    |                |
+------------------+---------------+------+-----+---------+----------------+
6 rows in set (0.001 sec)

MariaDB [esu]> DESC term_courses;
+-------------+---------+------+-----+---------+----------------+
| Field       | Type    | Null | Key | Default | Extra          |
+-------------+---------+------+-----+---------+----------------+
| term_crs_id | int(11) | NO   | PRI | NULL    | auto_increment |
| course_id   | int(11) | NO   | MUL | NULL    |                |
| term_id     | int(11) | NO   | MUL | NULL    |                |
| instructor  | int(11) | NO   | MUL | NULL    |                |
+-------------+---------+------+-----+---------+----------------+
4 rows in set (0.001 sec)

MariaDB [esu]> DESC terms;
+-------------+--------------+------+-----+---------+----------------+
| Field       | Type         | Null | Key | Default | Extra          |
+-------------+--------------+------+-----+---------+----------------+
| term_id     | int(11)      | NO   | PRI | NULL    | auto_increment |
| term_name   | varchar(56)  | NO   | UNI | NULL    |                |
| start_date  | date         | NO   |     | NULL    |                |
| end_date    | date         | NO   |     | NULL    |                |
| description | varchar(128) | NO   |     | NULL    |                |
+-------------+--------------+------+-----+---------+----------------+
5 rows in set (0.001 sec)
```

The solution seems to come from finding the `term_id` for the Fall Term and counting the distinct elements of the `course_id` column with the correct `term_id`.

I first ran `SELECT * from terms;` to get the right `term_id`:
```
+---------+------------+------------+------------+----------------------+
| term_id | term_name  | start_date | end_date   | description          |
+---------+------------+------------+------------+----------------------+
|       1 | SPRING2022 | 2022-04-04 | 2022-07-29 | Spring semester 2022 |
|       2 | FALL2022   | 2022-08-01 | 2022-11-25 | Fall semester 2022   |
+---------+------------+------------+------------+----------------------+
2 rows in set (0.000 sec)
```

The `term_id` for Fall 2022 is 2, so I finished with `SELECT COUNT(DISTINCT course_id) FROM term_courses WHERE term_id=2;` to get the answer of 405:
```
+---------------------------+
| COUNT(DISTINCT course_id) |
+---------------------------+
|                       405 |
+---------------------------+
1 row in set (0.004 sec)
```

Note that `DISTINCT` allows us to count unique elements.

`flag{405}`
