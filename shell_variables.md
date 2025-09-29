# SHELL VARIABLES
## 1. Printing variables
```
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{ERLXDBcb-A4zYi8VYwgGMMnqF-X.QX3UTN0wSMwEzNzEzW}
hacker@variables~printing-variables:~$ 
```
## 2. Setiing variables
```
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{QOmGobWdeBzFp_AxWX69hsGWgcD.QX5UTN0wSMwEzNzEzW}
hacker@variables~setting-variables:~$ 
```
## 3. Multi word variables
```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{UjAQYeUJea-16nakSzE9OSNK_Sp.QXwYTN0wSMwEzNzEzW}
hacker@variables~multi-word-variables:~$ 
```
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
