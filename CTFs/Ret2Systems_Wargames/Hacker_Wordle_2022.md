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

<br />

### 5. 







### FINAL solution for the win.  

![0905](/assets/img/ret2_wordle_solve.PNG)