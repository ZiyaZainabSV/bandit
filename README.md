# BANDIT WRITE UP 

**LEVEL 13 -> LEVEL 14** 

Password: 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL

Goal: The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on.

 Log in to bandit13
   1. Using command ls: One file called: sshkey.private 
   2. Changing directory to the one mentioned in the goal. 
   *Mistake*: Not a directory. 
   First using the command ls to see what's in the home directory. 
   Not of any use. 
   3. Finding /etc/bandit_pass/bandit14 and checking type of file. 
      1. *file /etc*: Directory
      2. *cd /etc*
      3. ls
      4. *find bandit_pass*: gives a list of several files.
      5. *file bandit_pass*: directory
      6. *cd bandit_pass*
      7. ls
      8. *file bandit14*: regular file, no read permission 
These steps are to be performed after logging into bandit14 
**Mistake**: Interpreted the question wrong. 
Login to bandit14: 
1. ls 
2. cat sshkey.private 
3. ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220 **Mistake** 

Reference: (https://help.ubuntu.com/community/SSH/OpenSSH/Keys)
Checked a writeup and saw that the format should have been bandit14@localhost 
4. ssh -i sshkey.private bandit14@localhost

Successfully logged into bandit14. 
5. cd .. : to change directory to home directory
6. cd /etc/bandit_pass
7. cat bandit14

Password successfully obtained!

**LEVEL 14 -> LEVEL 15**

Password: 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e

Goal: The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

1. Login to bandit14
2. *echo 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e | netcat localhost 30000* 
Returned password for next level!

Reference: (https://askubuntu.com/questions/443227/sending-a-simple-tcp-message-using-netcat)


**LEVEL 15 -> LEVEL 16**

Password: BfMYroe26WYalil77FoDi9qh59eK5xNr

Goal: The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

1. Login to bandit15
2. *echo BfMYroe26WYalil77FoDi9qh59eK5xNr | openssl s_client -connect localhost:30001* : **Mistake** Tried to approach the problem like with the previous level. 
3. *openssl s_client -connect localhost:30001*: A long output and in the end I was allowed to type whatever required. 
   1. *echo BfMYroe26WYalil77FoDi9qh59eK5xNr* : **Mistake** 

   2. *BfMYroe26WYalil77FoDi9qh59eK5xNr*: **Correct** Returned password for bandit16

Reference: (https://www.feistyduck.com/library/openssl-cookbook/online/ch-testing-with-openssl.html)

**LEVEL 16 -> LEVEL 17**

Password: cluFn7wTiGryunymYOu4RcffSxQluehd
