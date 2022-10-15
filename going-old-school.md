<h1>Going Old School</h1>

<h2>Problem</h2>
Unable to use their RSA encryption program, luciafer resorts to using old school techniques to send a message out to the team. Can you decipher the code and find the flag?

Submit the flag as flag{flag text}

Download Image
SHA1: 1afcf5cc3a64f3924f27425ed344fbe4545c5554

env.deadface.io

![Rendered Image](https://cyberhacktics.sfo2.digitaloceanspaces.com/DEADFACECTF2022/Challenges/crypto03/Old_School_sm.png)

<h2>Solution</h2>

The table on top threw me off for a bit because it was actually the tabula recta for the <a href="https://en.wikipedia.org/wiki/Beaufort_cipher">Beaufort Cipher,</a> not the Vigenere cipher. However, I eventually used a <a href="https://www.boxentriq.com/code-breaking/vigenere-cipher">Vigenere solver</a> to decode the ciphertext `DT UFAWDL IQYXFKVL` as `WE STRIKE TOMORROW` with key `hpcmjot`.

`flag{WE STRIKE TOMORROW}`

Note: The Braille on the bottom decodes to `PORT 47980`, but this information was uncessary for this specific challenge.
