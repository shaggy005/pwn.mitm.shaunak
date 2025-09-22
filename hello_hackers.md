# Hello Hackers Challenge – Writeup

The **Hello Hackers** challenge introduces some basic Linux command-line concepts.  
Below are the tasks, commands, and corresponding flags.

---

## 📑 Table of Contents
- [1. Intro to Commands](#1-intro-to-commands)
- [2. Intro to Arguments](#2-intro-to-arguments)
- [3. Command History](#3-command-history)
- [Summary](#summary)
- [References](#references)

---

## 1. Intro to Commands

This part demonstrates how to run a simple command.

```bash
hacker@hello~intro-to-commands:~$ whoami
hacker
```
The whoami command prints the current user. Here, the user is hacker.

```bash
hacker@hello~intro-to-commands:~$ hello
Success! Here is your flag:
pwn.college{kfOj1zhePUuNEF9ggGo3Gvhip2j.QX3YjM1wSMwEzNzEzW}
Flag: pwn.college{kfOj1zhePUuNEF9ggGo3Gvhip2j.QX3YjM1wSMwEzNzEzW}
```
Running the hello command reveals the flag.

## 2. Intro to Arguments
This part teaches that commands can take arguments.

```bash
hacker@hello~intro-to-arguments:~$ hello hackers
Success! Here is your flag:
pwn.college{wyQXvy3y6vjEZVpPKleRdzp67r3.QX4YjM1wSMwEzNzEzW}
Here, the command is hello, and the argument is hackers.
```
Supplying the argument correctly produces a new flag.

Flag: pwn.college{wyQXvy3y6vjEZVpPKleRdzp67r3.QX4YjM1wSMwEzNzEzW}

## 3. Command History
This part highlights the usefulness of checking the command history.

```bash
hacker@hello~command-history:~$ the flag is pwn.college{4DIY5zFtCaDnqbbNirapogK6Ws_.0lNzEzNxwSMwEzNzEzW}
```
The flag is directly revealed in the history.

Flag: pwn.college{4DIY5zFtCaDnqbbNirapogK6Ws_.0lNzEzNxwSMwEzNzEzW}

## Summary
Learned how to execute basic commands (whoami, hello).

Understood how to pass arguments to commands.

Explored command history.

## References
None
