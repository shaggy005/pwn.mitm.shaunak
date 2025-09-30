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

I created a new variable by assigning a value to it with PWN=COLLEGE. The challenge checked the value of my variable and gave me the flag.

### What I Learned:

I learned that in bash I can set variables using NAME=value with no spaces around the =. After that, I can access them with $NAME.

## 3. Multi word variables
```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{UjAQYeUJea-16nakSzE9OSNK_Sp.QXwYTN0wSMwEzNzEzW}
hacker@variables~multi-word-variables:~$ 
```

### Steps:

The challenge asked me to make a variable with multiple words. I did that by using quotes: PWN="COLLEGE YEAH". The quotes kept the words together as one value. The challenge confirmed it and gave me the flag.

### What I Learned:

I learned that if a variable value has spaces, I need to wrap it in quotes, otherwise the shell splits it up into separate words.

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

First, I set two variables: PWN=COLLEGE and COLLEGE=PWN. Then I exported PWN by running export PWN. After that, I ran /challenge/run, which checked my environment variables. Since PWN was exported (and COLLEGE wasn’t), the program confirmed the setup and gave me the flag.

### What I Learned:

I learned that export makes a variable part of the environment so that child processes (like /challenge/run) can access it. Variables that are not exported only stay in my current shell.

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

### Steps:

I used the command env to list all the environment variables. In the output, I found the FLAG variable, and its value was the flag.

### What I Learned:

I learned that env prints all the exported environment variables available to my shell. This is a useful way to check which variables have been exported.

## 6. Storing command output
```
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
Congratulations! You have read the flag into the PWN variable. Now print it out 
and submit it!
hacker@variables~storing-command-output:~$ echo $PWN
pwn.college{gB5tsTIVGCM0F_j0Kr2Jh7xYjrp.QX1cDN1wSMwEzNzEzW}
hacker@variables~storing-command-output:~$ 
```
### Steps:

I used command substitution to save the output of /challenge/run into a variable: PWN=$(/challenge/run). Then I ran echo $PWN to print its value, which was the flag.

### What I Learned:

I learned that I can capture the output of a command into a variable by using VAR=$(command). This is called command substitution, and it’s really useful when I want to store results for later use.

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

### Steps:

I used the read command to take input and store it in a variable. I typed read PWN, pressed enter, and then entered COLLEGE. The shell stored COLLEGE inside the variable PWN. The challenge verified it and gave me the flag.

### What I Learned:

I learned that the read command lets me store user input directly into a variable. This is especially useful when writing interactive shell scripts.

## 8. Reading files
```
hacker@variables~reading-files:~$ read PWN </challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{4mEFyxR-MzfN4v_I57FbGLl90aM.QXwIDO0wSMwEzNzEzW}
hacker@variables~reading-files:~$ 
```
### Steps:

Instead of typing input manually, I redirected a file into read. I ran read PWN </challenge/read_me, and the shell stored the file’s content into the variable PWN. The challenge confirmed it and gave me the flag.

### What I Learned:

I learned that I can use input redirection (<) to feed a file’s contents into commands. Combined with read, it lets me load file data directly into a variable.
