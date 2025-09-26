# FILE GLOBBING

## 1. Matching with *
```
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ ls /
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
bin   challenge  etc   home  lib32  libx32  mnt  opt   root  sbin  sys  usr
boot  dev        flag  lib   lib64  media   nix  proc  run   srv   tmp  var
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{cSUu410AlVM7wzzMqrBJJTa4KCm.QXxIDO0wSMwEzNzEzW}
hacker@globbing~matching-with-:/challenge$
```
## 2. Matching with ?
```
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{8LZ7G70R0DXmcjevOlmUXVxrO5h.QXyIDO0wSMwEzNzEzW}
hacker@globbing~matching-with-:/challenge$ 
```
## 3. Matching with []
```
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ echo file_[absh]
file_a file_b file_h file_s
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[absh]
You got it! Here is your flag!
pwn.college{Ums0SaLHBlfoFczPZ0O6HuORZ83.QXzIDO0wSMwEzNzEzW}
hacker@globbing~matching-with-:/challenge/files$ 
```
## 4. Matching paths with []
```
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[absh]
You got it! Here is your flag!
pwn.college{EnPm7nDmaXU6HSfKziY9JtwtxCY.QX0IDO0wSMwEzNzEzW}
hacker@globbing~matching-paths-with-:~$ 
```
## 5. Multiple Globs
```
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{sdDr6OVRE2NmWE9UWKoauckITo-.0lM3kjNxwSMwEzNzEzW}
hacker@globbing~multiple-globs:/challenge/files$ 
```
## 6. Mixing Globs
```
hacker@globbing~mixing-globs:~$ cd /challenge/files
/challenge/run [cep]*
You got it! Here is your flag!
pwn.college{wjF9pm2XEcsSShXmySLOljTd-yX.QX1IDO0wSMwEzNzEzW}
hacker@globbing~mixing-globs:/challenge/files$ 

```
## 7. Exclusion globbing
```
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
/challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{QZrvsOWd1Z1z5d2Unuw2gArYKgz.QX2IDO0wSMwEzNzEzW}
hacker@globbing~exclusionary-globbing:/challenge/files$ 
```
## 8. Tab Completion
```
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege​ 
pwn.college{Icw3RL8MabzYXiVSrak6e5cZeP8.0FN0EzNxwSMwEzNzEzW}
hacker@globbing~tab-completion:~$ 
```
## 9. Multiple options for tab completion
```
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwn
pwn                    pwn-the-planet         pwncollege-flag        pwncollege-flyswatter  
pwn-college            pwncollege-family      pwncollege-flamingo    pwncollege-hacking     
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-flag
pwn.college{Yif2zQ3FxbPcG7p5uRDYb-kVrv_.0lN0EzNxwSMwEzNzEzW}
hacker@globbing~multiple-options-for-tab-completion:~$ 
```
## 10. Tab completion on commands
```
hacker@globbing~tab-completion-on-commands:~$ pwncollege-21444 
Correct! Here is your flag:
pwn.college{UPthq2rOlBcLLSRuGpPFYo9YDr3.0VN0EzNxwSMwEzNzEzW}
hacker@globbing~tab-completion-on-commands:~$ 
```
