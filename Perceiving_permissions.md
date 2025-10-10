# Perceiving Permissions
## 1. Changing File Ownership
```
hacker@permissions~changing-file-ownership:~$ ls -l /flag
-r-------- 1 root root 60 Oct  9 18:09 /flag
hacker@permissions~changing-file-ownership:~$ cat /flag 2>/dev/null || echo "no read perms (expected)"
no read perms (expected)
hacker@permissions~changing-file-ownership:~$ chown hacker /flag || sudo chown hacker /flag
hacker@permissions~changing-file-ownership:~$ ls -l /flag
-r-------- 1 hacker root 60 Oct  9 18:09 /flag
hacker@permissions~changing-file-ownership:~$ cat /flag
pwn.college{EPdu2hhXo9vWMOMQa2SCpCo7TCq.QXxEjN0wSMwEzNzEzW}
hacker@permissions~changing-file-ownership:~$ 
```
### Steps

In this challenge, I learned how to change the ownership of a file using administrative privileges. I used the appropriate command to assign the file to the required user, which allowed me to access it successfully. Once the ownership was transferred, I verified it and accessed the contents to retrieve the flag.

### What I Learned

I learned that every file in Linux has an owner and a group associated with it. The owner determines who has control over the file and who can modify its permissions. The chown command can be used to change the file’s owner and group, and this is an essential concept for managing file access securely.

### References

man chown
## 2. Groups and Files
```
hacker@permissions~groups-and-files:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@permissions~groups-and-files:~$ ls -l /flag
-r--r----- 1 root root 60 Oct  9 18:14 /flag
hacker@permissions~groups-and-files:~$ chgrp hacker /flag
hacker@permissions~groups-and-files:~$ ls -l /flag
-r--r----- 1 root hacker 60 Oct  9 18:14 /flag
hacker@permissions~groups-and-files:~$ cat /flag
pwn.college{o4P9qyE21jm0MPm8tdU5IrDNjd6.QXxcjM1wSMwEzNzEzW}
hacker@permissions~groups-and-files:~$ 
```
### Steps

In this task, I changed the group ownership of a file to the required group so that members of that group could access it. After switching the file’s group, I confirmed the modification by listing its details and proceeded to open it to retrieve the flag.

### What I Learned

I learned that Linux uses groups to organize users and manage shared access to files. Group ownership defines which set of users can perform actions on a file based on the group permissions. The chgrp command helps in changing the group ownership efficiently.

### References

man chgrp
## 3. Fun With Groups Names
```
hacker@permissions~fun-with-groups-names:~$ id
uid=1000(hacker) gid=1000(grp18065) groups=1000(grp18065)
hacker@permissions~fun-with-groups-names:~$ id
uid=1000(hacker) gid=1000(grp18065) groups=1000(grp18065)
hacker@permissions~fun-with-groups-names:~$ id -gn
grp18065
hacker@permissions~fun-with-groups-names:~$ chgrp "$(id -gn)" /flag
hacker@permissions~fun-with-groups-names:~$ ls -l /flag
-r--r----- 1 root grp18065 60 Oct  9 18:16 /flag
hacker@permissions~fun-with-groups-names:~$ cat /flag
pwn.college{Q_Qou9xFpSa1QzEdPmaaJD2Xc1k.QXycjM1wSMwEzNzEzW}
hacker@permissions~fun-with-groups-names:~$ 
```
### Steps

This challenge required me to assign a file to a group that had a non-standard or tricky name. I carefully used the command syntax to include the correct group name and ensured it was recognized by the system. Once the change was successful, I was able to view the flag.

### What I Learned

I learned how Linux handles group names, including those with special characters or unusual formatting. This taught me to use proper quoting and syntax when referencing such groups. I also reinforced my understanding of how file ownership and group membership interact.

### References

man chown
## 4. Changing Permissions
```
hacker@permissions~changing-permissions:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@permissions~changing-permissions:~$ ls -l /flag
-r-------- 1 root root 60 Oct  9 18:19 /flag
hacker@permissions~changing-permissions:~$ chmod o+r /flag
hacker@permissions~changing-permissions:~$ ls -l /flag
-r-----r-- 1 root root 60 Oct  9 18:19 /flag
hacker@permissions~changing-permissions:~$ cat /flag
pwn.college{gO5zJXmNry0cJ8vlM3WelFPBLmR.QXzcjM1wSMwEzNzEzW}
hacker@permissions~changing-permissions:~$ 
```
### Steps

In this challenge, I needed to modify file permissions so that the necessary user or group could access and execute it. I examined the file’s existing permissions, then adjusted them appropriately to allow reading, writing, or execution as required to obtain the flag.

### What I Learned

I learned how Linux represents file permissions in symbolic (rwx) and numeric (octal) forms. Using the chmod command, I could precisely define what actions users, groups, and others are allowed to perform. Understanding this helped me grasp how access control works at a system level.

### References

man chmod
## 5. Executable Files
```
hacker@permissions~executable-files:~$ ls -l /challenge/run
-r--r--r-- 1 hacker hacker 32 Jan 14  2025 /challenge/run
hacker@permissions~executable-files:~$ chmod +x /challenge/run
hacker@permissions~executable-files:~$ ls -l /challenge/run
-r-xr-xr-x 1 hacker hacker 32 Jan 14  2025 /challenge/run
hacker@permissions~executable-files:~$ /challenge/run
Successful execution! Here is your flag:
pwn.college{0nHNI1kHmTeAsb-jIvfmQ8USQKX.QXyEjN0wSMwEzNzEzW}
hacker@permissions~executable-files:~$ 
```
### Steps

This level required me to make a file executable so that it could run as a program. I checked its current permissions, then added execution rights. After making it executable, I ran the file successfully to obtain the flag.

### What I Learned

I learned that in Linux, a file must have the execute (x) permission to be run as a program. Using chmod +x or the equivalent octal mode changes, I can grant execution privileges. This is an important concept for running scripts and binaries safely and effectively.

### References

man chmod
## 6. Permission Tweaking Practice
```
hacker@permissions~permission-tweaking-practice:~$ ls -l /challenge/pwn
-rw-r--r-- 1 hacker hacker 0 Oct  9 19:06 /challenge/pwn
hacker@permissions~permission-tweaking-practice:~$ stat -c '%A %a %n' /challenge/pwn
-rw-r--r-- 644 /challenge/pwn
hacker@permissions~permission-tweaking-practice:~$ chmod 640 /challenge/pwn && ls -l /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rw-r-----
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

You set the permissions incorrectly! Restarting the game!
-rw-r--r-- 1 hacker hacker 0 Oct  9 19:06 /challenge/pwn
hacker@permissions~permission-tweaking-practice:~$ chmod u=rwx,g=rx,o= /challenge/pwn && ls -l /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rwxr-x---
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

You set the permissions incorrectly! Restarting the game!
-rw-r--r-- 1 hacker hacker 0 Oct  9 19:06 /challenge/pwn
hacker@permissions~permission-tweaking-practice:~$ chmod g+w /challenge/pwn && ls -l /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rw-rw-r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

You set the permissions incorrectly! Restarting the game!
-rw-r--r-- 1 hacker hacker 0 Oct  9 19:06 /challenge/pwn
hacker@permissions~permission-tweaking-practice:~$ chmod o-x /challenge/pwn && ls -l /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

You set the permissions incorrectly! Restarting the game!
-rw-r--r-- 1 hacker hacker 0 Oct  9 19:06 /challenge/pwn
hacker@permissions~permission-tweaking-practice:~$ sudo chmod 640 /challenge/pwn && ls -l /challenge/pwn
sudo: workspace is not privileged
hacker@permissions~permission-tweaking-practice:~$ chmod 640 /challenge/pwn && stat -c '%A %a %n' /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rw-r-----
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

You set the permissions incorrectly! Restarting the game!
-rw-r--r-- 644 /challenge/pwn
hacker@permissions~permission-tweaking-practice:~$ chmod u=rw,g=r,o= /challenge/pwn && stat -c '%A %a %n' /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rw-r-----
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

You set the permissions incorrectly! Restarting the game!
-rw-r--r-- 644 /challenge/pwn
hacker@permissions~permission-tweaking-practice:~$ chmod o+r /flag && cat /flag 
/usr/bin/chmod: changing permissions of '/flag': Operation not permitted
NEEDED, BUT UNMET permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

You set the permissions incorrectly! Restarting the game!
hacker@permissions~permission-tweaking-practice:~$ chmod g+r /flag && cat /flag 
/usr/bin/chmod: changing permissions of '/flag': Operation not permitted
NEEDED, BUT UNMET permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

You set the permissions incorrectly! Restarting the game!
hacker@permissions~permission-tweaking-practice:~$ chmod 444 /challenge/pwn
You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxrwxrwx
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ ls -l /challenge/pwn
-r--r--r-- 1 hacker hacker 0 Oct  9 19:06 /challenge/pwn
hacker@permissions~permission-tweaking-practice:~$ stat -c '%A %a %n' /challenge/pwn
-r--r--r-- 444 /challenge/pwn
hacker@permissions~permission-tweaking-practice:~$ /challenge/run
Round 2 of 8!

Current permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxrwxrwx
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod 777 /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": rwxrwxrwx
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rwxrwxr-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod 777 /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": rwxrwxr-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rwxrwxrwx
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions

You set the permissions incorrectly! Restarting the game!
hacker@permissions~permission-tweaking-practice:~$ chmod 444 /challenge/pwn
You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": r--r--r--
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxrwxrwx
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod 777 /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": rwxrwxrwx
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rwxrwxr-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod 775 /challenge/pwn
You set the correct permissions!
Round 4 of 8!

Current permissions of "/challenge/pwn": rwxrwxr-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": -w-rwxr-x
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod 275 /challenge/pwn
You set the correct permissions!
Round 5 of 8!

Current permissions of "/challenge/pwn": -w-rwxr-x
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": -wxrwxr-x
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod 375 /challenge/pwn
You set the correct permissions!
Round 6 of 8!

Current permissions of "/challenge/pwn": -wxrwxr-x
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": --x--xr-x
- the user doesn't have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod 115 /challenge/pwn 
You set the correct permissions!
Round 7 of 8!

Current permissions of "/challenge/pwn": --x--xr-x
- the user doesn't have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": r-x--xr-x
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod 515 /challenge/pwn
You set the correct permissions!
Round 8 of 8!

Current permissions of "/challenge/pwn": r-x--xr-x
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": r-x------
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod 500 /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permission-tweaking-practice:~$ chmod u+r /flag && ls -l /flag && cat /flag
-r-------- 1 hacker hacker 60 Oct  9 19:06 /flag
pwn.college{AucHKem64nrXJveqd4w54drbm3j.QXwEjN0wSMwEzNzEzW}
hacker@permissions~permission-tweaking-practice:~$ 
```
### Steps

This challenge involved adjusting specific permission bits multiple times to meet a precise configuration. I practiced setting and removing read, write, and execute permissions for different user categories until the system verified the correct setup and granted the flag.

### What I Learned

I learned the importance of precision when modifying file permissions. Small mistakes, such as setting unnecessary permissions or omitting one, can cause either security risks or restricted access. This task strengthened my understanding of symbolic and numeric permission modifications.

### References
sameeeee
## 7. Permission Setting Practice
```
hacker@permissions~permissions-setting-practice:~$ chmod u=rw,g=r,o= /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": ---rwxrw-
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rw-r-----
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

You set the permissions incorrectly! Restarting the game!
hacker@permissions~permissions-setting-practice:~$ chmod u=rx,g=,o=rx /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": ---rwxrw-
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": r-x---r-x
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

You set the permissions incorrectly! Restarting the game!
hacker@permissions~permissions-setting-practice:~$ chmod u=rx,g=x,o= /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": ---rwxrw-
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": r-x--x---
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

You set the permissions incorrectly! Restarting the game!
hacker@permissions~permissions-setting-practice:~$ chmod a=rwx /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": ---rwxrw-
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rwxrwxrwx
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions

You set the permissions incorrectly! Restarting the game!
hacker@permissions~permissions-setting-practice:~$ chmod o= /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": ---rwxrw-
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rw-r-----
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

You set the permissions incorrectly! Restarting the game!
hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=r,o=r /challenge/pwn
NEEDED, BUT UNMET permissions of "/challenge/pwn": ---rwxrw-
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

CURRENT, INCORRECT permissions of "/challenge/pwn": rwxr--r--
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

You set the permissions incorrectly! Restarting the game!
hacker@permissions~permissions-setting-practice:~$ chmod 076 /challenge/pwn && ls -l /challenge/pwn && stat -c '%A %a %n' /challenge/pwn && /challenge/run
You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": ---rwxrw-
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r-x--x---
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
----rwxrw- 1 hacker hacker 0 Oct  9 19:41 /challenge/pwn
----rwxrw- 76 /challenge/pwn
Round 2 of 8!

Current permissions of "/challenge/pwn": ---rwxrw-
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r-x--x---
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod 510 /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": r-x--x---
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -wx-----x
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod 301 /challenge/pwn
You set the correct permissions!
Round 4 of 8!

Current permissions of "/challenge/pwn": -wx-----x
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rw--wx--x
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod 631 /challenge/pwn 
You set the correct permissions!
Round 5 of 8!

Current permissions of "/challenge/pwn": rw--wx--x
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": ---r-x-w-
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod 052 /challenge/pwn
You set the correct permissions!
Round 6 of 8!

Current permissions of "/challenge/pwn": ---r-x-w-
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rw--wx---
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod 630 /challenge/pwn
You set the correct permissions!
Round 7 of 8!

Current permissions of "/challenge/pwn": rw--wx---
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -w---xrw-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod 216 /challenge/pwn
You set the correct permissions!
Round 8 of 8!

Current permissions of "/challenge/pwn": -w---xrw-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxrwxrw-
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod 776 /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$
hacker@permissions~permissions-setting-practice:~$ chmod u+r /flag && ls -l /flag && cat /flag
-r-------- 1 hacker hacker 60 Oct  9 19:41 /flag
pwn.college{UcMiLkSvmZboRK5tVP-pudMzgk_.QXzETO0wSMwEzNzEzW}
hacker@permissions~permissions-setting-practice:~$ 
```
### Steps

In the final challenge of this section, I applied everything I had learned about ownership and permissions to configure files exactly as instructed. After setting the correct permissions and ownerships, I verified the setup and accessed the flag.

### What I Learned

I learned how ownership and permission settings work together to control access. This comprehensive exercise helped me become confident in using chown, chgrp, and chmod effectively. It also reinforced best practices for maintaining both functionality and security in Linux systems.

### References

man chown, man chmod, man chgrp
## 8. The SUID Bit
```
hacker@permissions~the-suid-bit:~$ ls -l /challenge/getroot
-rwxr-xr-x 1 root root 155 Jan 14  2025 /challenge/getroot
hacker@permissions~the-suid-bit:~$ file /challenge/getroot
/challenge/getroot: a /opt/pwn.college/bash script, ASCII text executable
hacker@permissions~the-suid-bit:~$ chmod +x /challenge/getroot
hacker@permissions~the-suid-bit:~$ chmod u+s /challenge/getroot
hacker@permissions~the-suid-bit:~$ ls -l /challenge/getroot
-rwsr-xr-x 1 root root 155 Jan 14  2025 /challenge/getroot
hacker@permissions~the-suid-bit:~$ stat -c '%A %a %n' /challenge/getroot
-rwsr-xr-x 4755 /challenge/getroot
hacker@permissions~the-suid-bit:~$ /challenge/getroot
SUCCESS! You have set the suid bit on this program, and it is running as root! 
Here is your shell...
root@permissions~the-suid-bit:~# cat /flag
pwn.college{IyuHvudYpeTNJoqbwjdzNZHmWjN.QXzEjN0wSMwEzNzEzW}
root@permissions~the-suid-bit:~# 
root@permissions~the-suid-bit:~# 
```
### Steps

In this challenge, I began by inspecting the file permissions of the program located at /challenge/getroot. Initially, it was owned by the root user and had standard executable permissions. I first ensured that the file was executable using the chmod +x command. Next, I set the SUID (Set User ID) bit on the file using chmod u+s. This special permission allows users to execute the file with the privileges of the file’s owner—in this case, root. After confirming the permission change with ls -l and stat, I ran the program. It successfully executed with root privileges, granting me a root shell. From there, I accessed and read the flag file, completing the challenge.

### What I Learned

I learned about the SUID permission bit in Linux and how it can temporarily elevate user privileges during program execution. The SUID bit, represented by an “s” in the owner’s execute field (e.g., -rwsr-xr-x), enables a file to run as its owner rather than the user who executes it. This mechanism is often used by system binaries like passwd to perform administrative operations securely. However, I also learned that misconfiguring SUID bits can create serious security vulnerabilities, as it allows privilege escalation if exploited.

### References

man chmod
