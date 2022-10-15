<h1>First Strike</h1>

<h2>Problem</h2>
There was a cyber attack on ESU's website on July 27th. ESU IT staff collected data from the attack and need your help sifting through it.

What IP Address did the attack originate from? Submit the flag as: flag{ip_address}. Example: flag{192.168.1.1}.

Download access.log
SHA1: b71d59350a6802b9fc1b772a76388ca250ba6d89

Download error.log
SHA1: 8fc2c50a21e7133c319c6bb4df597cc707f21c91
<h2>Solution</h2>
The only IP address in the <code>access.log</code> file is <code>165.227.73.138</code>.

<code>flag{165.227.73.138}</code>

<h1>Toolbox</h1>

<h2>Problem</h2>
What tool was used when the attack started at 2022-07-27 14:13 UTC? Submit the flag as flag{tool}. Example: flag{notepad}.

Use the files from First Strike.

<h2>Solution</h2>
Looking at the user agents for the timestamp 14:13 UTC, we see that Nmap was used.

<code>flag{nmap}</code>

<h1>Agents of Chaos</h1>

<h2>Problem</h2>
What is the first user agent of the second scanning tool used by the attacker? Submit the flag as flag{user agent string}.

Use the files from First Strike.
<h2>Solution</h2>
The second scanning tool was Nikto starting at 14:15:13, and the user agent was "Mozilla/5.00 (Nikto/2.1.6) (Evasions:None) (Test:Port Check)."

<code>flag{Mozilla/5.00 (Nikto/2.1.6) (Evasions:None) (Test:Port Check)}</code>

<h1>Iterations</h1>

<h2>Problem</h2>
What is the name of the tool that likely resulted in DEADFACE acquiring login credentials to ESU's website?

Submit the flag as flag{tool}.

Use the files from First Strike.
<h2>Solution</h2>
Looking at this <a href="https://ghosttown.deadface.io/t/ready-set-go/50/4">GhostTown thread,</a> spookyboi mentions that he used hydra to find a common password.

<code>flag{hydra}</code>
