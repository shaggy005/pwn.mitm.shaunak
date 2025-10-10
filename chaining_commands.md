# Chaining Commands
## 1. Chaining with semicolons
```
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn ; /challenge/college 
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{EgI0SOylYOMaNeg9bDkH8y7i-ZI.QX1UDO0wSMwEzNzEzW}
hacker@chaining~chaining-with-semicolons:~$ 
```
### Steps

I executed two commands back-to-back so they would run one after the other regardless of whether the first succeeded or failed. After running both in sequence, the challenge acknowledged the chaining and revealed the flag.

### What I Learned

I learned that the semicolon operator lets me run multiple commands sequentially without depending on the success or failure of earlier commands. It’s useful for sequencing independent steps in a workflow.

### References
literally no reference was needed

## 2. Building on Success
```
hacker@chaining~building-on-success:~$ /challenge/first-success && /challenge/second
Nice chaining! Flag: pwn.college{YXy5TH3rKkxFbGroAhG-T4BlTYa.0lM0MDOxwSMwEzNzEzW}
hacker@chaining~building-on-success:~$ 
```
### Steps

I ran a command that needed to succeed first, and only when it completed successfully I executed a follow-up command. The challenge used that success-dependent chaining to confirm the correct behavior and return the flag.

### What I Learned

I learned how the logical AND operator works to run a second command only if the first returns a zero exit status. This is extremely useful for creating safe, conditional multi-step pipelines.

### References

Shell operator && documentation

## 3. Handling Failure
```
hacker@chaining~handling-failure:~$ /challenge/first-failure || /challenge/second
Nice chaining! Flag: pwn.college{sSoXO-iQdwJISXiItmQz7mklgQ_.01M0MDOxwSMwEzNzEzW}
hacker@chaining~handling-failure:~$ 
```
### Steps

I structured two commands so that the second would run only if the first failed. The challenge detected this failure-dependent logic and provided the flag when the fallback was executed.

### What I Learned

I learned that the logical OR operator allows conditional fallback behavior: run the next command only when the previous one fails (nonzero exit). This pattern is handy for recoveries and alternatives in scripts.

### References

Shell operator || documentation

Error-handling patterns in shell scripting
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
### Steps

I wrote a small shell script that ran a sequence of challenge commands, saved the script, then executed it. The script ran both steps in the intended order and the challenge validated my script, returning the flag.

### What I Learned

I learned how to create a basic shell script, how scripts are executed by an interpreter, and how packaging repeated commands into a script improves reproducibility and clarity.

### References

documentation to shell scripting (shebang, script files)

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
### Steps

I created a script that produced output and then piped the script’s output into the challenge’s checker. By redirecting the script’s stdout into the validator, the challenge confirmed the output and returned the flag.

### What I Learned

I learned how to redirect or pipe a script’s output into another program, which is essential for composing tools and automating verification tasks. This reinforced how scripts integrate into pipelines.

### References

I/O redirection and pipes in shell scripting

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
### Steps

I wrote a script, made it executable, and then ran it directly from the filesystem. The script executed as a standalone program, produced the expected behavior, and the challenge awarded the flag.

### What I Learned

I learned that marking a script as executable allows it to be run directly, and that the system will invoke the interpreter specified by the script’s shebang (or default shell). Making scripts executable is the standard way to distribute command-line tools.

### References

Executable permission and script execution semantics

chmod and script execution guides
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
### Steps

I created a script that started with a shebang line indicating which interpreter should run it, made the file executable, and executed it. The challenge tested the script and confirmed that using the correct interpreter header worked, giving me the flag.

### What I Learned

I learned how the shebang line tells the kernel which interpreter to use to execute the script, ensuring predictable behavior across environments. This is important for portability and for writing scripts that rely on specific shells or interpreters.

### References

Shebang (#!) explanation and best practices
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
### Steps

I wrote a script that accessed positional parameters and validated their order/values according to the challenge requirements. After making it executable and running the test, the challenge verified the argument handling and returned the flag.

### What I Learned

I learned how shell scripts receive command-line arguments as positional parameters, how to reference them inside the script, and how to manipulate or reorder them when needed. This is foundational for writing flexible command-line tools.

### References

Shell positional parameters ($1, $2, etc.)

Shell script argument-handling tutorials
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
### Steps

I wrote a script that used a conditional check to compare an argument against an expected value and printed output accordingly. I then executed the script in the challenge environment; the script’s conditional behavior matched the requirements and the flag was awarded.

### What I Learned

I learned how to implement basic if conditionals in shell scripts to control flow based on runtime values. Conditional logic is crucial to validating inputs and branching behavior in automation scripts.

### References

Shell if syntax and comparison operators

Scripting best practices for conditionals
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
### Steps

I extended conditional logic with an else clause to handle default cases when the test condition wasn’t met. After making the script executable, the challenge validated both branches (the conditional and the default) and returned the flag.

### What I Learned

I learned how to structure if/else statements to provide sensible defaults and fallback behavior when inputs don’t match expected cases. This makes scripts more robust and user-friendly.

### References
uhm idk same shit

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
### Steps

I implemented a script that used elif branches to handle multiple different input cases and produce distinct outputs for each. After testing the various inputs, the challenge confirmed the script correctly handled all the conditions and provided the flag.

### What I Learned

I learned how elif extends simple if conditionals to cover multiple discrete cases cleanly, avoiding nested conditionals and improving readability. This is useful for command-line utilities that must support different modes.

### References

Complex condition handling with if/elif/else in shell

Readability guidelines for shell scripts
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
### Steps

I inspected the challenge’s script to learn how it accepted input and what exact string it expected. Then I provided the correct input string to the program (as the script specified) and the challenge recognized the correct answer and revealed the flag.

### What I Learned

I learned that reading and understanding existing scripts is often the fastest path to solving script-driven puzzles: the script itself may contain the required inputs, formats, or passwords. This reinforced the habit of inspecting program source before guessing inputs.

### References

Techniques for reading and understanding shell scripts

Secure scripting and auditing practices
