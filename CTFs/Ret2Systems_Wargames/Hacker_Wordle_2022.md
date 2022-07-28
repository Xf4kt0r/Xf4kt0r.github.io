# Ret2 Systems: Hacker Wordle  

## The RET2 SYSTEMS corporation re-wrote the wildly popular game Wordle in its favorite language: C. Now the game is blazing fast, but is it secure?  

## To solve this challenge, you must pop a shell and exfiltrate the flag.  

<br />

### DISCLAIMER: I did not complete all of the work myself while solving this challenge. I followed along with John Hammond's live video here:  

### <a href="https://www.youtube.com/watch?v=BGIW6Vx3Mq8" target="_blank">Hacking Wordle ?! x64 "pwn" Binary Exploitation - RET2 WarGames Platform</a>

### pausing along the way and trying to figure things out. I was able to pop the shell after some of his knowledgable nudging and interestingly enough, I used a slightly different character set to get shell.  

<br />

### 1. Watch the video and access the <a href="https://wargames.ret2.systems/levels#Demo#shmoo2022_pwn" target="_blank">Wordle PWN Demo</a>.  

<br />

### 2. Pause when necessary, try things out.  

<br />

### 3. John got me through a few things that would have likely taken me quite a while but when he stumbled upon the **18**, it hit me.  

<br />

### 4. I did some python xor'ing and messing around with characters to see how they were ending up on the stack.    

```
>>> chr(0x18 ^ 0x29)
'1'
>>> chr(0x1c ^ 0x29)
'5'
>>> chr(0x1d ^ 0x29)
'4'
>>> chr(0x1a ^ 0x29)
'3'
>>> chr(0x1b ^ 0x29)
'2'
>>> chr(0x6d ^ 0x29)
'D'
>>> chr(0x19 ^ 0x29)
'0'
>>> chr(0x6f ^ 0x29)
'F'
>>> chr(0x1c ^ 0x29)
'5'
>>> chr(0x1d ^ 0x29)
'4'
>>> chr(0x7f ^ 0x29)
'V'
>>> chr(0xff ^ 0x29)
'Ö'
>>> chr(0x5e ^ 0x29)
'w'
>>> chr(0x6e ^ 0x29)
'G'
>>> chr(0x40 ^ 0x29)
'i'
>>> chr(0x00 ^ 0x29)
')'
>>> chr(0x19 ^ 0x29)
'0'
>>> chr(0x40 ^ 0x29)
'i'
>>> chr(0x0d ^ 0x29)
'$'
>>> chr(0xd2 ^ 0x29)
'û'
```

<br />

### 5. I had previously tried sending non alphanumeric charcters which worked so I knew I could likely send others get the correct address results for the `ret2system` function.  

![ret2_wordle_xoring.PNG](/assets/img/ret2_wordle_xoring.PNG "RET2 Wordle Xor'ing")

<br />

### 6. Now it came down to shifing these charcters to get them to fall in place to pop the shell.  

### FINAL SOLUTION FOR THE WIN!  

![ret2_wordle_solve.PNG](/assets/img/ret2_wordle_solve.PNG "RET2 Wordle Solve")