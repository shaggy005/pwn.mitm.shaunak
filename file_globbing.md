FILE GLOBBING

# 1. Matching with *
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
# 2. Matching with ?
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
