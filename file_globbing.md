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
### Steps

Listed the root directory with ls /.

Used cd /ch* to match /challenge with a * glob.

Verified the directory change worked.

Ran /challenge/run to get the flag.

### What I Learned

* is a wildcard glob that matches zero or more characters.

Using * can shorten paths like /ch* → /challenge.

This is useful, but also risky if it matches unintended files.

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
### Steps

Used cd /?ha??enge where ? represents any single character.

This matched /challenge.

Ran /challenge/run inside /challenge.

### What I Learned

? matches exactly one character.

Multiple ? can be chained to match multiple characters.

Useful for precise matching of unknown file names.
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
### Steps

Navigated to /challenge/files.

Used echo file_[absh] to expand into file_a file_b file_h file_s.

Ran /challenge/run file_[absh] to capture the flag.

### nWhat I Learned

[] defines a set of characters that can match one position.

[absh] matches any of a, b, s, or h.

A clean way to pick subsets of filenames.
## 4. Matching paths with []
```
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[absh]
You got it! Here is your flag!
pwn.college{EnPm7nDmaXU6HSfKziY9JtwtxCY.QX0IDO0wSMwEzNzEzW}
hacker@globbing~matching-paths-with-:~$ 
```
### Steps

Directly passed /challenge/files/file_[absh] to /challenge/run.

This expanded into the required files.

Got the flag.

### What I Learned

[] globs also work with full paths, not just filenames.

Globbing happens before the command runs, so expansions are inserted into the argument list.
## 5. Multiple Globs
```
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{sdDr6OVRE2NmWE9UWKoauckITo-.0lM3kjNxwSMwEzNzEzW}
hacker@globbing~multiple-globs:/challenge/files$ 
```
### Steps

Went to /challenge/files.

Ran /challenge/run *p*.

The *p* glob matched all filenames containing p.

Got the flag.

### What I Learned

You can use multiple * in a single pattern (*p*).

This matches any file containing the given substring.

Globbing can be combined flexibly for complex searches.
## 6. Mixing Globs
```
hacker@globbing~mixing-globs:~$ cd /challenge/files
/challenge/run [cep]*
You got it! Here is your flag!
pwn.college{wjF9pm2XEcsSShXmySLOljTd-yX.QX1IDO0wSMwEzNzEzW}
hacker@globbing~mixing-globs:/challenge/files$ 
```
### Steps

Changed into /challenge/files.

Used /challenge/run [cep]* to match filenames starting with c, e, or p.

Ran successfully and got the flag.

### What I Learned

Globs can be combined: [] to restrict the start, * for the rest.

[cep]* means "any file starting with c, e, or p".

Short globs can capture multiple target files at once.
## 7. Exclusion globbing
```
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
/challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{QZrvsOWd1Z1z5d2Unuw2gArYKgz.QX2IDO0wSMwEzNzEzW}
hacker@globbing~exclusionary-globbing:/challenge/files$ 
```
### Steps
Went to /challenge/files.

Used /challenge/run [!pwn]* to match files not starting with p, w, or n.

Got the flag.

### What I Learned

! inside [] negates the set.

[!pwn] matches any first character except p, w, or n.

Useful to exclude unwanted matches when globbing.
## 8. Tab Completion
```
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege​ 
pwn.college{Icw3RL8MabzYXiVSrak6e5cZeP8.0FN0EzNxwSMwEzNzEzW}
hacker@globbing~tab-completion:~$ 
```
### Steps

Tried to manually type /challenge/pwncollege but failed.

Used Tab after typing /challenge/pwn to auto-complete the tricky filename.

Successfully ran cat /challenge/pwncollege and got the flag.

### What I Learned

Tab completion saves time and prevents typos.

It can reveal tricky characters or hidden symbols in filenames.

Tab completion is safer than using * for sensitive commands (like rm).
## 9. Multiple options for tab completion
```
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwn
pwn                    pwn-the-planet         pwncollege-flag        pwncollege-flyswatter  
pwn-college            pwncollege-family      pwncollege-flamingo    pwncollege-hacking     
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-flag
pwn.college{Yif2zQ3FxbPcG7p5uRDYb-kVrv_.0lN0EzNxwSMwEzNzEzW}
hacker@globbing~multiple-options-for-tab-completion:~$ 
```
### Steps

Typed cat /challenge/files/pwn and hit Tab.

Multiple completions were suggested (pwn-college, pwncollege-flag, etc.).

Picked the correct one: pwncollege-flag.

Read the file and got the flag.

### What I Learned

If there are multiple matches, pressing Tab twice lists them all.

You can type more characters to disambiguate, then press Tab again.

Very useful for navigating directories with similar names.
## 10. Tab completion on commands
```
hacker@globbing~tab-completion-on-commands:~$ pwncollege-21444 
Correct! Here is your flag:
pwn.college{UPthq2rOlBcLLSRuGpPFYo9YDr3.0VN0EzNxwSMwEzNzEzW}
hacker@globbing~tab-completion-on-commands:~$ 
```
### Steps

At the shell, typed pwncollege- and pressed Tab.

Tab completion suggested available commands (like pwncollege-21444).

Executed the suggested command.

Got the flag.

### What I Learned

Tab completion works for commands as well as files.

Helps discover available binaries in $PATH.

Useful in CTFs for finding hidden or randomized command names.
