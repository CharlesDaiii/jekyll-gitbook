# Hacking 101 Course Artifact - Ruiyang Dai

This course used CTF problem and CVEs to aid in acquiring new skills and knowledge.

This assignment is to create a knowledge writeup of what you learned through the CTFs and each of the CVEs.  The writeup consists of two sections:

**Section 1: CTFs.** 

1. Describe what you came into the course knowing as 1 paragraph overview.
    
    I only knew some basic knowledge about binary and assembly code. I never heard of Capture the Flag by the time the course started. Although I have experience using tools like gdb to debug my c code, I have never tried to exploit programs.
    
2. a bullet per CTF problem on what you had to do to solve the problem. 
    1. New Orleans: The key to solving the challenge is to realize that the **`create_password`** routine writes a sequence of bytes, which, when converted to ASCII, reveal the required password. I solved this one using my previous knowledge.
    2. Sydney: The critical insight is that the CPU stores values in little endian format in memory, and the password must be rearranged accordingly. It took me some time to remember the little endian, which is quite confusing at first.
    3. Hanoi: The key is to enter a password that overflows the buffer and manipulates a specific memory address to pass a comparison check. After I have done this one, I found myself easily overflowed the attack lab in the course 18613.
    4. Cusco: By providing a password longer than 16 characters, it's possible to corrupt the stack when the **`login`** function returns. I never tried to use long characters to solve the CTF, and after this one, I always tried some long characters to see if this might work.
    5. Reykjavik: by ensuring the password buffer starts with **`0xdb01`** in little endian format, the conditional check can be passed, resulting in the lock being unlocked.
    6. Whitehorse: The task is to enter a password that causes a stack overflow and redirects code execution to the shellcode, which unlocks the lock without verification from the Hardware Security Module (HSM).
    7. Montevideo: The highlight involves using a password payload that includes shellcode to manipulate the program's execution flow and unlock the lock.
    8. Johannesburg: The solution involves crafting a password payload that includes the canary value **`0x6a`** at the right position and then appending the little endian formatted address of the **`unlock_door`** routine.
    9. Santa Cruz: the challenge is cracked by carefully crafting a username payload to override specific bytes for bounds checking and to adjust the return address.
    10. Jakarta: By entering a username of 32 'A's and a password that overflows to more than 255 characters, including a specific payload to overwrite the return address, the length check is bypassed.
    11. Addis Ababa: The key is to craft an input string that uses format specifiers to manipulate memory values. The solution involves using **`%n`** in the input string to write specific values to memory, thereby bypassing security checks.
    12. Novosibirsk: Firstly, I tried the method from last CTF Addis Ababa. By using the **`%n`** format specifier in the **`printf()`** function, it's possible to write to arbitrary memory locations. This technique is utilized to manipulate specific memory addresses to unlock the door.
    13. Algiers: This CVE took me a long time to solve. The key step involves overflowing the password field, which corrupts the header of the password's chunk and causes a faulty memory access. This is achieved by input manipulation that allows control over certain memory addresses.

**Section 2: CVEs.** 

1. Describe what you came into the course knowing about CVEs, then a paragraph per CVE that you did as part of your group, then a summary.  (10 points each).
    
    I didn’t know CVEs when I came into the course. At the beginning, I thought CVEs are far away from me, which needs a lot of experience and knowledge to solve. However, after going through all CVEs we presented in the course, I gradually understand the mechanics and the effort behind CVEs, and it became much more familiar to me on looking through PoCs and exploits.
    
    **Group 7 CVE set 1**
    
    In the first set, we chose a topic about dirty pipe. When we were doing research about this CVE, I don’t really have experience with CVEs. So I was just randomly looking through materials and articles from internet. Fortunately, we found an article about how the dirty pipe was found out in an maintenance. I read and understood the article and discussed the issues described in the article with my teammates. Then Minhao and I searched for the specific version of VM so that we can reproduce that vulnerability and exploit it using the code we found on Github. In the presentation, I gave a speech about how these concepts are connected together under this vulnerability, and I introduced the story to everyone in the class to aware them how his vulnerability had indeed harmed people and properties.  
    
    **Group 7 CVE set 2**
    
    In the second set, we chose a topic about Winrar. Since we are at the end of this set, our group took a long time to decide which topic is interesting. Heba and I persuaded other people on this topic we chose, because I felt Winrar is a software that people all have experience with. After the topic was determined, I searched on the internet looking for PoCs as well as how this vulnerability is triggered. This is the hardest one I had been working on, since Winrar is not an open source software. We had to think of ways to patch the software ourselves because winrar won’t publish what they have done on their code to fix the vulnerable part.
    
    **Group 2 CVE set 3**
    
    In the last set, we combined 2 topic together, which are about c_rehash in Openssl and mlflow. In this set, our team don’t have much time to prepare since we only have 2 days to finish the presentation (we are traveling back from Thanks giving, and there are 4 people in our group just done their last CVE just before the break). Instead of randomly picking a easy one, we decided to combine two CVE together so that it makes our presentation more interesting and more innovative. I build the Windows runtime environment for this CVE. Zhijia Yang and I worked on the code and terminal to create a working demo. In the presentation, I also researched on how this vulnerability of OpenSSL had impact other softwares and the industry.