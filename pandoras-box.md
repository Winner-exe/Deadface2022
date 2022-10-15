<h1>Pandora's Box</h1>

<h2>Problem</h2>
Pandora's box, we have found it! Even better, the last travelers knew the numbered code to get in but they couldn't figure out the transcription. Figure out the the transcription's translation to find the flag!

Download Image
SHA1: 8e613787658d2d5828448aa182e2bb4904c124a8

Submit the flag as: flag{word_word_word_word}

![Rendered Image](https://cyberhacktics.sfo2.digitaloceanspaces.com/DEADFACECTF2022/Challenges/crypto09/pandoras_box.PNG.png)
<h2>Solution</h2>
This seems to be a simple substitution cipher where each letter gets shifted to the right by the corresponding number to encode the message. After applying the reverse translation on each letter, I got that the message was `DONT LET HER OUT`.

`flag{DONT LET HER OUT}`
