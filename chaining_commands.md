# Chaining COmmands
## 1. Chaining with semicolons
```
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn ; /challenge/college 
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{EgI0SOylYOMaNeg9bDkH8y7i-ZI.QX1UDO0wSMwEzNzEzW}
hacker@chaining~chaining-with-semicolons:~$ 
```
## 2. Building on Success
```
hacker@chaining~building-on-success:~$ /challenge/first-success && /challenge/second
Nice chaining! Flag: pwn.college{YXy5TH3rKkxFbGroAhG-T4BlTYa.0lM0MDOxwSMwEzNzEzW}
hacker@chaining~building-on-success:~$ 
```
## 3. Handling Failure
```
hacker@chaining~handling-failure:~$ /challenge/first-failure || /challenge/second
Nice chaining! Flag: pwn.college{sSoXO-iQdwJISXiItmQz7mklgQ_.01M0MDOxwSMwEzNzEzW}
hacker@chaining~handling-failure:~$ 
```
## 4. Your first shell script
```
hacker@chaining~your-first-shell-script:~$ cat > x.sh <<'EOF'
> /challenge/pwn
> /challenge/college
> EOF
hacker@chaining~your-first-shell-script:~$ cat x.sh

/challenge/pwn

/challenge/college

hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{Uk35vHzpeqhJG53CmCEN-CSraOO.QXxcDO0wSMwEzNzEzW}
hacker@chaining~your-first-shell-script:~$ 
```
## 5. Redirecting Script Output
```
hacker@chaining~redirecting-script-output:~$ cat > x.sh <<'EOF'
> /challenge/pwn
> /challenge/college
> EOF
hacker@chaining~redirecting-script-output:~$ cat x.sh

/challenge/pwn

/challenge/college

hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{oflRAUT7cgfcqqvWJsc-f0x7zJK.QX4ETO0wSMwEzNzEzW}
hacker@chaining~redirecting-script-output:~$ 
```
## 6. Executable shell scripts
```
hacker@chaining~executable-shell-scripts:~$ cat > x.sh <<'EOF'
> script -q -c "/challenge/solve" /dev/null <<'INPUT'
> PWN
COLLEGE
INPUT
EOF

hacker@chaining~executable-shell-scripts:~$ chmod +x x.sh
hacker@chaining~executable-shell-scripts:~$ ./x.sh

PWN
COLLEGE
Congratulations on your shell script execution! Your flag:
pwn.college{8ffk3zcyZFujOsU5ObSa79dF4Qt.QX0cjM1wSMwEzNzEzW}
hacker@chaining~executable-shell-scripts:~$ 

```
# 7. Understanding Shebangs
```
hacker@chaining~understanding-shebangs:~$ printf '%s\n' '#!/bin/bash' 'echo "hack the planet"' > /home/hacker/solve.sh
hacker@chaining~understanding-shebangs:~$ chmod +x /home/hacker/solve.sh
hacker@chaining~understanding-shebangs:~$ sed -n '1p' /home/hacker/solve.sh
#!/bin/bash
hacker@chaining~understanding-shebangs:~$ cat -v /home/hacker/solve.sh          
#!/bin/bash
echo "hack the planet"
hacker@chaining~understanding-shebangs:~$ /home/hacker/solve.sh
hack the planet
hacker@chaining~understanding-shebangs:~$ /challenge/run
Testing your script...
Perfect! Your flag:
Flag: pwn.college{sWJzCFFLaF3SFqZVTnyF4-1pVk-.0VOzMDOxwSMwEzNzEzW}

hacker@chaining~understanding-shebangs:~$
```
## 8. Scripting with arguments
```
hacker@chaining~scripting-with-arguments:~$ printf '%s\n' '#!/bin/bash' 'printf "%s %s\n" "$2" "$1"' > /home/hacker/solve.sh
hacker@chaining~scripting-with-arguments:~$ chmod +x /home/hacker/solve.sh
hacker@chaining~scripting-with-arguments:~$ /challenge/run
Correct! Your script properly reversed the arguments.
Here's your flag:
pwn.college{gZjQLItuOUgMNQwQmU8rHC8ix3A.0VNzMDOxwSMwEzNzEzW}
hacker@chaining~scripting-with-arguments:~$ 
```
## 9. Scripting with conditionals
```
hacker@chaining~scripting-with-conditionals:~$ printf '%s\n' '#!/bin/bash' 'if [ "$1" = "pwn" ]; then echo "college"; fi' > /home/hacker/solve.sh
hacker@chaining~scripting-with-conditionals:~$ chmod +x /home/hacker/solve.sh
hacker@chaining~scripting-with-conditionals:~$ /challenge/run
Correct! Your script properly handles all the conditions.
Here's your flag:
pwn.college{0YnGmhGHmvTJtF1VUdzh_GTfsti.0lNzMDOxwSMwEzNzEzW}
hacker@chaining~scripting-with-conditionals:~$ 
```
## 10. Scripting with default cases
```
hacker@chaining~scripting-with-default-cases:~$ printf '%s\n' '#!/bin/bash' 'if [ "$1" = "pwn" ]; then echo "college"; else echo "nope"; fi' > /home/hacker/solve.sh
hacker@chaining~scripting-with-default-cases:~$ chmod +x /home/hacker/solve.sh
hacker@chaining~scripting-with-default-cases:~$ /challenge/run
Correct! Your script properly handles the if/else conditions.
Here's your flag:
pwn.college{siZt4haO-4cQulLPY1amcKgYLmh.01NzMDOxwSMwEzNzEzW}
hacker@chaining~scripting-with-default-cases:~$ 
```
## 11. Scripting with multiple conditions
```
hacker@chaining~scripting-with-multiple-conditions:~$ printf '%s\n' '#!/bin/bash' 'if [ "$1" = "hack" ]; then' '  echo "the planet"' 'elif [ "$1" = "pwn" ]; then' '  echo "college"' 'elif [ "$1" = "learn" ]; then' '  echo "linux"' 'else' '  echo "unknown"' 'fi' > /home/hacker/solve.sh
hacker@chaining~scripting-with-multiple-conditions:~$ chmod +x /home/hacker/solve.sh
hacker@chaining~scripting-with-multiple-conditions:~$ /challenge/run
Correct! Your script properly handles all the conditions with elif.
Here's your flag:
pwn.college{kSRzpyixqhff61Jj3rHzXDpkNxH.0FOzMDOxwSMwEzNzEzW}
hacker@chaining~scripting-with-multiple-conditions:~$ 
```
## 12. Reading shell scripts
```
hacker@chaining~reading-shell-scripts:~$ cat /challenge/run
#!/opt/pwn.college/bash

read GUESS
if [ "$GUESS" == "hack the PLANET" ]
then
        echo "CORRECT! Your flag:"
        cat /flag
else
        echo "Read the /challenge/run file to figure out the correct password!"
fi
hacker@chaining~reading-shell-scripts:~$ printf 'hack the PLANET\n' | /challenge/run
CORRECT! Your flag:
pwn.college{U_BvFueu3pR0CM3GDm4KaKUJ_tp.0lMwgDOxwSMwEzNzEzW}
hacker@chaining~reading-shell-scripts:~$ 
```
