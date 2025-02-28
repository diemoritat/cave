---
lastSync: Thu Jun 27 2024 11:57:47 GMT+0530 (India Standard Time)
---
# Intro-Rev (Reverse engineering challenge)

This challenge gave a bin file (a C file). The challenge said the binary will give the flag just by running. But when we run, it just printed the first line. I asked Chatgpt to suggest me some logics. Then I used Radare2 to print out the main function.

![[intro-rev.png]]

1. pdf @main - command to print the login of main in assembly.
2. aaa - to analyse the bin.

I input this logic to chatgpt and asked for explanation. Chatgpt said that this main function prints out the whole flag. But it sleeps for 724911 seconds on each run. So we need to seek to the memory address where there is call to sleep function, then we need to nop it. 

3. s <address> - to seek that address (here: sleep 0x000011ab [sleep function call])
   4. wx 9090909090 - 90 is the opcode for nop. since there is 5 bytes in sleep. we have put 9090909090.
   5. q - to quit r2.

The commands will null the sleep function and save it. after this, when we run the chall file. It will print the whole flag without sleeping.