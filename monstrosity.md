<h1>Monstrosity</h1>

<h2>Problem</h2>
We found this program written by mirveal. He used it to hide a password in the form of a flag. See if you can find the flag in the program.

Download File
SHA1: 4452cfb82b7d6f3027cfe2a75f9281be8610a94a

Submit the flag as flag{flag_text}.

<h2>Solution</h2>

After downloading the `monstrosity` file, I ran `file monstrosity` to find out more about it:
```
> file monstrosity  
monstrosity: ELF 64-bit LSB executable, x86-64, version 1 (GNU/Linux), statically linked, no section header
```

This shows that monstrosity is an executable, so I ran `./monstrosity`:
```

    __  ___                 __                  _ __       
   /  |/  /___  ____  _____/ /__________  _____(_) /___  __
  / /|_/ / __ \/ __ \/ ___/ __/ ___/ __ \/ ___/ / __/ / / /
 / /  / / /_/ / / / (__  ) /_/ /  / /_/ (__  ) / /_/ /_/ / 
/_/  /_/\____/_/ /_/____/\__/_/   \____/____/_/\__/\__, /  
                                                  /____/   

A dreaded beast that slumbers in its secret lair, remaining in a dormant state for centuries.
>  Cyclops

Incorrect.
```

Looks like this program is looking for a very specific input. I was stuck at this point for a while and could not get any useful information about the program, but eventually after solving the OSINT challenge "Under Public Scrutiny," I noticed that the public repo was named "tarrasque." After a quick Google search, I found that the tarrasque is actually a monster, so I tried inputting "Tarrasque" into the program:
```
    __  ___                 __                  _ __       
   /  |/  /___  ____  _____/ /__________  _____(_) /___  __
  / /|_/ / __ \/ __ \/ ___/ __/ ___/ __ \/ ___/ / __/ / / /
 / /  / / /_/ / / / (__  ) /_/ /  / /_/ (__  ) / /_/ /_/ / 
/_/  /_/\____/_/ /_/____/\__/_/   \____/____/_/\__/\__, /  
                                                  /____/   

A dreaded beast that slumbers in its secret lair, remaining in a dormant state for centuries.
>  Tarrasque

You are correct.
flag{TaRrAsqUE_m0nstros1tY}
```

`flag{TaRrAsqUE_m0nstros1tY}`
