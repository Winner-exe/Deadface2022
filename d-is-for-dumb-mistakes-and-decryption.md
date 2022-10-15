<h1>D is for Dumb Mistakes</h1>

<h2>Problem</h2>

To show off their 1337 programming skills, DEADFACE attempted to create their own encryption process to help them communicate privately. Although the encryption process is working, the decryption process is flawed. The De Monne security team was able to find DEADFACE's code and can see that they are trying to use the RSA algorith with these variables:

Prime numbers of 1049 and 2063
Exponent of 777887
Recompute the decryption key (d) and submit the flag as flag{d=VALUE}

<h2>Solution</h2>

This was a straightforward application of textbook RSA. Using Python, I calculated $n=1049\cdot 2063$ and $\phi(n)=1048\cdot 2062,$ then applied the Extended Euclidean Algorithm to find the inverse of $777887 \mod{n}.$ This returned the flag $d=1457215.$

<code>flag{d=1457215}</code>

<h1>D is for Decryption</h1>

<h2>Problem</h2>

Now that you know the correct RSA decryption value d from "D" is for Dumb Mistakes, can you use it to properly decrypt one of DEADFACE's private messages? The ciphertext that De Monne's security team intercepted was:

992478-1726930-1622358-1635603-1385290

Assuming each - character separates each letter of the ciphertext and every letter in the alphabet is represented by its position (i.e., a = 1, b = 2, etc.), what is the plaintext version of this message? Submit the flag as flag{plaintext}.

<h2>Solution</h2>

Another straightforward application of RSA. Using the value of $d$ from before, I took each number $c$ from the ciphertext and calculated $c^d\mod{n}$, then converted the numbers to ASCII alphabetic characters to get that the plaintext was <code>ghost</code>.

<code>flag{ghost}</code>.
