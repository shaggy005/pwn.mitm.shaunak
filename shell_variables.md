# SHELL VARIABLES
## 1. Printing variables
```
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{ERLXDBcb-A4zYi8VYwgGMMnqF-X.QX3UTN0wSMwEzNzEzW}
hacker@variables~printing-variables:~$ 
```

### Steps:

I noticed that the variable FLAG was already set in my environment. I printed it using echo $FLAG, and it displayed the flag value.

### What I Learned:

I learned that I can access the value of a variable by prefixing it with $. For example, echo $FLAG prints whatever is stored inside FLAG.


## 2. Setiing variables
```
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{QOmGobWdeBzFp_AxWX69hsGWgcD.QX5UTN0wSMwEzNzEzW}
hacker@variables~setting-variables:~$ 
```

### Steps:

You created a variable by assigning a value to it.

Example: PWN=COLLEGE

The challenge checked your variable and confirmed the correct setup, giving you the flag.

### What I Learned:

Variables in bash are set with NAME=value (no spaces around =).

Once set, you can use them like $NAME.

## 3. Multi word variables
```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{UjAQYeUJea-16nakSzE9OSNK_Sp.QXwYTN0wSMwEzNzEzW}
hacker@variables~multi-word-variables:~$ 
```

### Steps:

The challenge asked for a variable with multiple words.

You set it like this:

PWN="COLLEGE YEAH"

The quotes ensured the shell treated "COLLEGE YEAH" as a single value, not two separate words.

The challenge confirmed the variable and rewarded the flag.

### What I Learned:

Use quotes when assigning multi-word strings to variables.

Without quotes, the shell would split words by spaces and cause errors.

## 4. Exporting variables
```
hacker@variables~exporting-variables:~$ PWN=COLLEGE
You've set the PWN variable to the proper value!
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ export PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great 
job! Here is your flag:
pwn.college{A-6wa0y4s0_sOn-xfGNTiiV05D5.QXyYTN0wSMwEzNzEzW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ 
```

### Steps:

You first set variables:

PWN=COLLEGE

COLLEGE=PWN

Then you exported PWN using:

export PWN

Exporting made the variable visible to child processes (like /challenge/run).

When you ran /challenge/run, it verified the setup and gave you the flag.

### What I Learned:

export makes a variable part of the environment, so other programs/commands can see it.

Variables set without export only exist inside the current shell session.

## 5. Printing exported variables
```
hacker@variables~printing-exported-variables:~$ env
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
MANPATH=/run/dojo/share/man:
DOJO_AUTH_TOKEN=b7de8cf2106f8095ea0ca80784441d9d637949be2938acef3057de20b9b8db92
HOME=/home/hacker
LANG=C.UTF-8
FLAG=pwn.college{AJlHhZFQJT5PuzW6CzN4v17pyDF.QX4UTN0wSMwEzNzEzW}
TERMINFO=/run/dojo/share/terminfo
TERM=xterm-256color
SHLVL=2
LC_CTYPE=C.UTF-8
SSL_CERT_FILE=/run/dojo/etc/ssl/certs/ca-bundle.crt
PATH=/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
DEBIAN_FRONTEND=noninteractive
_=/run/dojo/bin/env
hacker@variables~printing-exported-variables:~$ 
```

Steps:

You ran:

env

This printed all exported environment variables.

Among them, you spotted the FLAG variable with its value (the flag).

What I Learned:

The env command lists all environment variables available to the current shell.

This is how you can see what’s been exported and available globally.

## 6. Storing command output
```
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
Congratulations! You have read the flag into the PWN variable. Now print it out 
and submit it!
hacker@variables~storing-command-output:~$ echo $PWN
pwn.college{gB5tsTIVGCM0F_j0Kr2Jh7xYjrp.QX1cDN1wSMwEzNzEzW}
hacker@variables~storing-command-output:~$ 
```
## 7. Reading input
```
hacker@variables~reading-input:~$ echo PWN="COLLEGE"
PWN=COLLEGE
hacker@variables~reading-input:~$ read PWN
COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{cultdd7gCwxqv8t3R6c3wThKHiu.QX4cTN0wSMwEzNzEzW}
hacker@variables~reading-input:~$ 
```
## 8. Reading files
```
hacker@variables~reading-files:~$ read PWN </challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{4mEFyxR-MzfN4v_I57FbGLl90aM.QXwIDO0wSMwEzNzEzW}
hacker@variables~reading-files:~$ 
```
