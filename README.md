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

Goal: The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it. 

1. Finding which ports in the given range are listening
 
*nmap -p 31000-32000 localhost*
Returns the following ports: 
   1. 31046
   2. 31518 
   3. 31691
   4. 31790
   5. 31960

Reference: (https://securitytrails.com/blog/best-port-scanners)

2. Finding out which of the ports speak SSL

Using *openssl s_client -connect localhost:**port*** : Gave the following when connected to port 31790

-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----


**LEVEL 17 -> LEVEL 18**

Goal: There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

1. Create a .key file to store the key in.
*touch bandit17.key*
*echo **key** >> bandit17.key*

2. Login to bandit17 using the key. 
*ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220* : **Mistake** The permissions for bandit17.key are too open. 
**Correction**: 
Changing permission to read, write for owner and none for other users: *chmod 400 bandit17.key*
*ssh -i bandit17.key bandit17@bandit.labs.overthewire.org* 

3. Retrieving password: 
*diff passwords.new passwords.old*

**LEVEL 18 -> LEVEL 19**

Password: kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd

1. Tried logging into bandit18 but got automatically logged out. 

2. *ssh -t bandit18@bandit.labs.overthewire.org bash --norc --noprofile*
Let me type in commands
Reference: (https://serverfault.com/questions/94503/login-without-running-bash-profile-or-bashrc)

bash --noprofile: Does not read the .bashrc file. (i.e any of the startup or personal initialization files)
--norc: Do not read and execute the initialization files. 
  *ls* 
  *cat readme*: Gave password 

**LEVEL 19 -> LEVEL 20**

Password: IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x

1. Login
2. Tried using several tutorials, didn't work. 
3. Checked a writeup
*ls*
**only bandit20-do in list**
*./bandit20-do cat /etc/bandit_pass/bandit20* 
Gave password. 
The ./ executes the file. Since only bandit20-do can execute /etc/bandit_pass/bandit20, the statement ./bandit20-do should be used to read the file. 

**LEVEL 20 -> LEVEL 21**

Password: GbKksEFF4yrVs6il55v6gwY5aVje5f0j

1. Login
2. Checking what all ports are listening
*nmap -p localhost*: Did not work 
*nmap localhost* : Gave list of listening ports
3. Creating a new port for listening
*nc -l 40000*: Gave no output. Had to terminate command (using ctrl+C)
*nc -l 40000 &* : The command got executed
4. Confirming that the port was created 
*nstat -anlp |grep 40000*: No output 
5. Checked a writeup
*echo "GbKksEFF4yrVs6il55v6gwY5aVje5f0j" | nc -l -p 40000* 
Opened a new terminal (mentioned in the writeup but not in the website). 
*nmap localhost -p 40000* : Shows that the port is open
6. *./suconnect 40000*: Could not connect 

**STARTING OVER**

1. Creating a new port to connect to suconnect
Problem solved! The port closed too quickly the first time 
*./suconnect 50000* : Gave password in the other terminal. 

Reference: (https://kongwenbin.wordpress.com/2016/09/07/overthewire-bandit-level-20-to-level-21/)

**LEVEL 21 -> LEVEL 22**

Password: gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr

1. Login
2. Reading manuals for cron, crontab and crontab(5)
3. *crontab -u bandit21 cron.d*: cron.d not a regular file
4. *crontab -u bandit21 -l*: No permission. -l lists user's crontabs 
5. *ls -la* : In the list, there is a file called cronjob_bandit22
*crontab -u bandit21 cronjob_bandit22*: No permission
6. *cat cronjob_bandit22*: Listed some file /usr/bin/cronjob_bandit22.sh
7. *cat /usr/bin/cronjob_bandit22.sh*: The command being executed is chmod and then cat. 
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
The password may be in /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
8. *cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv* : Gave password

References: (https://www.jonyschats.nl/writeups/bandit-level-21-to-22/)
(https://phoenixnap.com/kb/how-to-list-display-view-all-cron-jobs-linux)

**LEVEL 22 -> LEVEL 23**

Password: Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
