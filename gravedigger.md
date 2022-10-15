<h1>Grave Digger 2</h1>

<h2>Problem</h2>
A member of DEADFACE has a sensitive file on d34th's machine. See if you can find a way to read the gravedigger2 file. Submit the flag as flag{flag text}.

env.deadface.io Password: 123456789q

Use context from Grave Digger 1

<h2>Solution</h2>
Using crypto_vamp's password, I was able to ssh into d34th's machine using `ssh crypto_vamp@env.deadface.io`.

crypto_vamp doesn't have anything in his home directory, so I went snooping around other places.

In `/opt`, I managed to find a file named `reader` created by `lilith`, another Deadface member:
```
crypto_vamp@1f7d7b95ed62:/opt$ ls -l
total 16
-rwsr-xr-x 1 lilith lilith 13016 Sep 25 16:28 reader
```

I found that reader was an executable with the following usage:
```
crypto_vamp@1f7d7b95ed62:/opt$ ./reader
Usage: reader [OPTIONS] [FILENAME]
```

The `reader` has its own manpage, too:
```
crypto_vamp@1f7d7b95ed62:/opt$ man reader
man(8)                                                                                                     reader man page                                                                                                     man(8)

NAME
       reader - read files as lilith

SYNOPSIS
       reader [OPTIONS] [FILENAME]

DESCRIPTION
       reader is developed to help crypto_vamp and other new recruits read privileged files until their vetting process is complete.

OPTIONS
       -f, --file FILENAME
              Read the contents of FILENAME.

       -c, --command COMMAND
              Execute a command (for troubleshooting purposes ONLY).

       -h, --help
              View the help information.

       -v, --version
              View the version information.

       BUGS   No known bugs.

AUTHOR
       Lilith (bl0ody_mary@deadface.io)

1.3.1                                                                                                        24 Sep 2022                                                                                                       man(8)
```

This allows crypto_vamp to read and execute files as lilith!

Going to lilith's home Documents directory, I found that there were two files:
```
crypto_vamp@1f7d7b95ed62:/home/lilith/Documents$ ls -l
total 8
-rw-rw---- 1 lilith lilith 2031 Oct 13 22:45 gravedigger2
-rw-rw---- 1 lilith lilith  993 Oct 13 22:46 gravedigger2.png.txt
```

Running the reader program, I was able to find the following:
```
crypto_vamp@1f7d7b95ed62:/home/lilith/Documents$ /opt/reader -f gravedigger2
█████████████████████████████████████
█████████████████████████████████████
████ ▄▄▄▄▄ █▄██▄█▀▀▄▀██▀ █ ▄▄▄▄▄ ████
████ █   █ █▀ ▀█ ▀  ▀▄▄▄▄█ █   █ ████
████ █▄▄▄█ █   ▀▀▀█▄▄▀▀▀██ █▄▄▄█ ████
████▄▄▄▄▄▄▄█ ▀▄█▄█ ▀▄▀ █▄█▄▄▄▄▄▄▄████
████ ▀▀█ █▄ ▄▀ ▀ ▄ ▀▄▄▄▄▀  ▄ ▄▀█ ████
█████ █  █▄▀ █▀██ ▄ ▀ ▀▀▄ ▄██ ▄█ ████
████ ▀  █ ▄▄ █▀█  ▀▀▄▄▄▄▀▀▀▄▀▀██▀████
████▄▀ ▀▀▄▄▀ ▀ ███▀ ▄▀▄▀▀█▄▄▄ ▄▀ ████
████▀▄▀ ▄█▄▀█▄▀▄█▄▄▀▄▄▄▄▄▀▀▄▀▄▀▄ ████
██████▄█ ▀▄█▄██ ▄ ▄▄▄ ▄██▄▀▀███▀▄████
████▄▄█▄█▄▄█ ▄██▀ ▀▀▄▄▄▄ ▄▄▄ ▀▀▄▀████
████ ▄▄▄▄▄ █▄ ▀  █▀▄ ▀▀▄ █▄█ ▄█▀▄████
████ █   █ █▄▄█▄  ▄▀▀▄▄  ▄▄ ▄▀▀▄▀████
████ █▄▄▄█ ██▀ █▀█▀▄▀  ▄▀▀▀▄███  ████
████▄▄▄▄▄▄▄█▄▄▄██▄▄█▄▄▄█▄▄▄████▄█████
█████████████████████████████████████
▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀
```
Scanning the QR code gives the flag.

`flag{d1091652793d0f31f53164353b6414e9}`

Note: The manpage gives lilith's email address (bl0ody_mary@deadface.io), which is the flag for the bonus challenge "Contact."

`flag{bl0ody_mary@deadface.io}`
