### Untangling Users
## 1. Becoming root with su
```
hacker@users~becoming-root-with-su:~$ su
Password: 
root@users~becoming-root-with-su:/home/hacker# ls
COLLEGE  PWN  instructions  myflag        pwn
Desktop  f    mid_output    not-the-flag  the-flag
root@users~becoming-root-with-su:/home/hacker# cat instructions 
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will check that error output is redirected to a specific file path : instructions
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!

[TEST] You should have redirected my stderr to instructions. Checking...

[PASS] The file at the other end of my stderr looks okay!
[PASS] Success! You have satisfied all execution requirements.
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{I1qX3AxFqlDfudNKWO3ccqSNlBa.QX1UDN1wSMwEzNzEzW}
root@users~becoming-root-with-su:/home/hacker# 

```
### Steps

In this challenge, I switched to the root user using the su command and entered the password when prompted. Once I gained root access, I examined the files in the home directory and read the instructions provided. The instructions explained that both standard output and error output needed to be redirected to specific files for verification. After ensuring the outputs were redirected correctly, the challenge confirmed that all requirements were satisfied and revealed the flag.

### What I Learned

I learned how the su command allows a user to assume another user’s identity—most notably the root user—to gain administrative privileges. I also understood the importance of redirecting standard output (stdout) and standard error (stderr) streams to specific files, which is essential in many Linux scripting and debugging tasks.

### References

man su

## 2. Other users with su
```
hacker@users~other-users-with-su:~$ su zardus
Password: 
zardus@users~other-users-with-su:/home/hacker$ ls
COLLEGE  PWN  instructions  myflag        pwn
Desktop  f    mid_output    not-the-flag  the-flag
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{U9bcDCOO3ITcyB8STWHNjEJLgCN.QX2UDN1wSMwEzNzEzW}
zardus@users~other-users-with-su:/home/hacker$ 
```
### Steps

In this task, I was required to switch from my current user to another user named zardus. I used the su command followed by the username and entered the correct password. Once logged in as Zardus, I executed the challenge program, which confirmed my identity and displayed the flag.

### What I Learned

I learned how su can be used to switch between different user accounts within the same system. This concept helped me understand user privileges, authentication, and the separation of access rights between accounts. It also highlighted the importance of password protection and least-privilege principles in multi-user environments.

### References

man su
## 3. Cracking passwords
```
hacker@users~cracking-passwords:~$ cat /challenge/shadow-leak
root:*:20182:0:99999:7:::
daemon:*:20182:0:99999:7:::
bin:*:20182:0:99999:7:::
sys:*:20182:0:99999:7:::
sync:*:20182:0:99999:7:::
games:*:20182:0:99999:7:::
man:*:20182:0:99999:7:::
lp:*:20182:0:99999:7:::
mail:*:20182:0:99999:7:::
news:*:20182:0:99999:7:::
uucp:*:20182:0:99999:7:::
proxy:*:20182:0:99999:7:::
www-data:*:20182:0:99999:7:::
backup:*:20182:0:99999:7:::
list:*:20182:0:99999:7:::
irc:*:20182:0:99999:7:::
gnats:*:20182:0:99999:7:::
nobody:*:20182:0:99999:7:::
_apt:*:20182:0:99999:7:::
systemd-timesync:*:20357:0:99999:7:::
systemd-network:*:20357:0:99999:7:::
systemd-resolve:*:20357:0:99999:7:::
mysql:!:20357:0:99999:7:::
messagebus:*:20357:0:99999:7:::
sshd:*:20357:0:99999:7:::
hacker::20357:0:99999:7:::
zardus:$6$59qOrWqabQt4rKmh$05bVRW75KmmYLuueESsoqxv6rFIjBv3m94oJFrdSFDSliS.AQQ.s88yHZN./Wps7XX.T6VTd887wgyj2D3i6B1:20370:0:99999:7:::
hacker@users~cracking-passwords:~$ awk -F: '/^zardus:/{print $2}' /challenge/shadow-leak > zardus.hash
hacker@users~cracking-passwords:~$ cat zardus.hash
$6$59qOrWqabQt4rKmh$05bVRW75KmmYLuueESsoqxv6rFIjBv3m94oJFrdSFDSliS.AQQ.s88yHZN./Wps7XX.T6VTd887wgyj2D3i6B1
hacker@users~cracking-passwords:~$ john ./zardus.hash
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
aardvark         (?)
1g 0:00:00:10 100% 2/3 0.09775g/s 281.5p/s 281.5c/s 281.5C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@users~cracking-passwords:~$ --shaow
bash: --shaow: command not found
hacker@users~cracking-passwords:~$ --show
bash: --show: command not found
hacker@users~cracking-passwords:~$ john --show
Password files required, but none specified
hacker@users~cracking-passwords:~$ john ./zardus.hash --show
?:aardvark

1 password hash cracked, 0 left
hacker@users~cracking-passwords:~$ su zardus
Password: 
su: Authentication failure
hacker@users~cracking-passwords:~$ su zardus
Password: 
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{UhLA3HslG7wM3PvyesBuGsCJ1Jv.QX3UDN1wSMwEzNzEzW}
zardus@users~cracking-passwords:/home/hacker$ 
```
### Steps

This challenge involved a password hash leak in a file resembling the /etc/shadow format. I identified the entry belonging to the user zardus and extracted the hashed password using awk. I saved it in a separate file and then used the john (John the Ripper) tool to crack the hash. The cracked password was revealed as “aardvark.” After obtaining the password, I used su zardus to log in as Zardus and successfully executed the challenge to retrieve the flag.

### What I Learned

I learned how Linux stores user password hashes in the /etc/shadow file and how tools like John the Ripper can be used to crack those hashes through brute force or dictionary attacks. This helped me understand the importance of password hashing algorithms like SHA-512 and the necessity of strong password policies to prevent compromise. I also learned practical command-line techniques for parsing and isolating sensitive data.

### References
yadayadayada idk just solved it from the question

## 4. Using sudo
````
hacker@users~using-sudo:~$ sudo -l
User hacker may run the following commands on users~using-sudo:
    (ALL) NOPASSWD: ALL
hacker@users~using-sudo:~$ sudo -i
root@users~using-sudo:~# 
root@users~using-sudo:~# whoami
root
root@users~using-sudo:~# cat /flag /challenge/flag /home/*/flag 2>/dev/null || /challenge/run
pwn.college{oYLLFsK2NCzhbHYb5r6fBTCkLts.QX4UDN1wSMwEzNzEzW}
In the olden days, a typical Linux system had a `root` password that administrators would use to `su` to root (after logging into their account with their normal account password).
But `root` passwords are a pain to maintain, they (or their hashes!) can leak, and they don't lend themselves well to larger environments (e.g., fleets of servers).
To address this, in recent decades, the world has moved from administration via `su` to administration via `sudo` (*Fun Fact*: `sudo` originally stood for **su**peruser **do**, but has changed to "`su` 'do'", and because `su` stands for "substitute user", the current meaning of `sudo` is "substitute user, do").

Unlike `su`, which defaults to launching a shell as a specified user, `sudo` defaults to running a command as `root`:

```console
hacker@dojo:~$ whoami
hacker
hacker@dojo:~$ sudo whoami
root
hacker@dojo:~$
```

Or, more relevant to getting flags:

```console
hacker@dojo:~$ grep hacker /etc/shadow
grep: /etc/shadow: Permission denied
hacker@dojo:~$ sudo grep hacker /etc/shadow
hacker:$6$Xro.e7qB3Q2Jl2sA$j6xffIgWn9xIxWUeFzvwPf.nOH2NTWNJCU5XVkPuONjIC7jL467SR4bXjpVJx4b/bkbl7kyhNquWtkNlulFoy.:19921:0:99999:7:::
hacker@dojo:~$
```

Unlike `su`, which relies on password authentication, `sudo` checks policies to determine whether the user is authorized to run commands as `root`.
These policies are defined in `/etc/sudoers`, and though it's mostly out of scale for our purposes, there are plenty of [resources](https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file) for learning about this!

So, the world has moved to `sudo` and has (for the purposes of system administration) left `su` behind.
In fact, even pwn.college's Practice Mode works by giving you `sudo` access to elevate privileges!

In this level, we will give you `sudo` access, and you will use it to read the flag.
Nice and easy!

----
**NOTE:**
After this level, we will enable Privileged Mode!
When you launch a challenge in Privileged Mode (by clicking the `Privileged` button instead of the `Start` button), the resulting container will give you full `sudo` access to allow you to introspect and debug to your heart's content, but of course with a placeholder flag.
root@users~using-sudo:~# 
````
### Steps

In this challenge, I checked the commands I was allowed to run using sudo without entering a password. The output showed that I had unrestricted sudo privileges. I used sudo -i to open a root shell and verified my identity as root. From there, I accessed the flag directly by reading it from the given file paths, completing the task successfully.

### What I Learned

I learned how sudo works as a safer and more controlled alternative to su. Instead of switching users entirely, it allows the execution of specific commands with elevated privileges based on configured policies in the /etc/sudoers file. I also understood the difference between privilege escalation using su (password-based) and sudo (policy-based), and how modern Linux systems rely on sudo for system administration.

### References

man sudo and man sudoers
