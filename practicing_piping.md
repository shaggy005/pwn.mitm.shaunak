# Practicing Piping
## 1. Redirecting Output
```
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your 
flag:
pwn.college{g-0eOx2R7GPHAPyvYHqMkFiUjGh.QX0YTN0wSMwEzNzEzW}
hacker@piping~redirecting-output:~$
```
### Detailed steps

In a shell, type: echo PWN > COLLEGE.

echo writes PWN to stdout.

> tells the shell to open (create/truncate) the file COLLEGE and connect the command's stdout to that file.

Verify the file contents: cat COLLEGE should show PWN.

If cat shows nothing or permission denied, check the working directory and ls -l COLLEGE for permissions/ownership.

To append instead of replace, use >>: echo MORE >> COLLEGE.

### What I learned

> redirects stdout (file descriptor 1) and truncates the file (creates it if necessary).

Redirection is performed by the shell before the command runs.

Use >> to append. Be careful not to accidentally overwrite (>).

File permissions and the shell's current directory matter — if you cannot create the file, choose a directory you own (e.g., your home or /tmp).

## 2. Redirecting more output
```
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{QpC5l0Ki8Xskp4YMh2QUPOuVAD_.QX1YTN0wSMwEzNzEzW}

hacker@piping~redirecting-more-output:~$ 

```
### Detailed steps

Run the program with stdout redirected: /challenge/run > myflag.

The shell opens myflag for writing (truncates if present), then executes /challenge/run with fd1 pointing to myflag.

When the program finishes, read the file: cat myflag.

Troubleshooting: If myflag is empty, confirm the program wrote to stdout (not only to stderr) and check that the program actually ran successfully (exit status: echo $?).

### What I learned

Redirecting to a file captures what the program writes to stdout.

Use absolute paths to avoid confusion (e.g., /home/hacker/myflag).

If the program writes only to stderr, > won't capture it — use 2> or 2>&1 as needed.

## 3. Appending output
```
hacker@piping~appending-output:~$ /challenge/run>> /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do 
the first write directly to the file, and the second write, I'll do to stdout 
(if it's pointing at the file). If you redirect the output in append mode, the 
second write will append to (rather than overwrite) the first write, and you'll 
get the whole flag!
hacker@piping~appending-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{QpC5l0Ki8Xskp4YMh2QUPOuVAD_.QX1YTN0wSMwEzNzEzW}

hacker@piping~appending-output:~$ cat the-flag
 | 
\|/ This is the first half:
 v 
pwn.college{oJWhVUWZCfY0FQJo0vG2glH_Yy-.QX3ATO0wSMwEzNzEzW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>) 
rather than *append* mode (>>), and so the write of the second half to stdout 
overwrote the initial write of the first half directly to the file. Try append 
mode!
hacker@piping~appending-output:~$
```
### Detailed steps

Use append mode so that multiple writes land in the same file without overwriting: /challenge/run >> /home/hacker/the-flag.

If the program writes first directly to the file and then writes to stdout, appending ensures both parts are preserved.

Verify with cat /home/hacker/the-flag.

If you accidentally used > and saw only half the data, rerun with >>.

If a program uses internal file-descriptor tricks (e.g., opening its own file descriptors), that can affect behavior — many challenges warn about FD_CLOEXEC and how python may set it.

### What I learned

>> opens the file in append mode; writes will be added to the end.

When a program writes some data to a file and some to stdout, append mode can be used to catch both pieces without losing the first.

Be aware some languages/programs change FD inheritance behavior (FD_CLOEXEC). That matters if you're trying to pass open FDs between processes.

## 4. Redirecting errors
```
hacker@piping~appending-output:~$ /challenge/run>> /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do 
the first write directly to the file, and the second write, I'll do to stdout 
                                                                                                                                                                Connected!
hacker@piping~redirecting-errors:~$ /challenge/run >myflag 2>instructions
hacker@piping~redirecting-errors:~$ cat instructions
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
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{YgO2XONyEopTPGtcJXKuBu1fCW5.QX3YTN0wSMwEzNzEzW}
```
### Detailed steps

To split stdout and stderr into separate files: /challenge/run > myflag 2> instructions.

> redirects fd1 (stdout).

2> redirects fd2 (stderr).

Check instructions to see program’s diagnostic messages: cat instructions.

Check myflag to see the program’s normal output: cat myflag.

If you want both in the same file: /challenge/run >combined 2>&1 or /challenge/run &>combined (bash-specific).

### What I learned

2> is used to capture stderr (fd2); stdout and stderr are separate streams.

The order of 2>&1 matters: cmd >out 2>&1 combines both into out. If you write cmd 2>&1 >out you'll not get the intended result.

For portability, prefer cmd >out 2>&1 in shells that support it.

# 5. Redirecting Input
```
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < OWN
bash: OWN: No such file or directory
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read 
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{4mGg46mUPDjSymZEvcN8-LosVoJ.QXwcTN0wSMwEzNzEzW}
hacker@piping~redirecting-input:~$
```
### Detailed steps

Create the input file: echo COLLEGE > PWN.

Run the program with its stdin connected to that file: /challenge/run < PWN.

The program reads from fd0 (stdin) and uses the contents as if the user had typed them.

If you see No such file or directory, confirm file exists (ls -l PWN) and you used the correct filename.

For inline input you can also use a here-document: ./program <<EOF\nline1\nline2\nEOF.

### What I learned

< redirects stdin (fd0) so the process reads from the file instead of the terminal.

Useful to automate interactions where a program reads from stdin.

Using wrong filenames or working directories is a common cause of failure.

# 6. Grepping Stored Results
```
hacker@piping~grepping-stored-results:~$ /challenge/run > /temp.data.txt
bash: /temp.data.txt: Permission denied
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep pwn.college /tmp/data.txt
pwn.college{soGsc50dY3V6NT8Zn4FBzYXRUXa.QX4EDO0wSMwEzNzEzW}
hacker@piping~grepping-stored-results:~$
```
### Detailed steps

Avoid writing to root-owned paths you do not own — use /tmp or your home directory: /challenge/run > /tmp/data.txt.

Inspect the saved output: less /tmp/data.txt or cat /tmp/data.txt.

Search for the flag string using grep: grep pwn.college /tmp/data.txt.

If you need a unique temporary filename, use mktemp.

### What I learned

Some directories (e.g., /) need root privileges — prefer /tmp or $HOME when experimenting.

Storing long output to a file makes it easy to search later with grep, sed, awk.

grep is fast for simple string searches; use -i for case-insensitive or -E for regex.

## 7. Grepping live output
```
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{o-pBvoyHAkJncFw-vZYzcOqaaxR.QX5EDO0wSMwEzNzEzW}
```
### Detailed steps

Pipe the program's stdout directly into grep: /challenge/run | grep pwn.college.

This launches both processes; grep reads lines from the upstream process and prints those matching the pattern.

If nothing is printed, check if the upstream program buffers output. Many programs buffer differently when writing to a pipe instead of a terminal.

To force line-buffered output for some programs, use stdbuf -oL (if available): stdbuf -oL /challenge/run | grep pwn.college.

### What I learned

| connects fd1 of the left process to fd0 of the right process — standard stream piping.

Output buffering can hide results when piping; stdbuf or unbuffer can help.

The checker may verify that the program on the other end is actually grep (path matters); which grep shows the path you will use.

## 8. Grepping errors
```
hacker@piping~grepping-errors:~$ /challenge/run 2>&1 | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{sD2JPEFxkjG5ZaYDX36l0ItLkyj.QX1ATO0wSMwEzNzEzW}
hacker@piping~grepping-errors:~$ 
```

### Detailed steps

To capture both stdout and stderr and pass them to another program: /challenge/run 2>&1 | grep pwn.college.

2>&1 makes stderr go to the same place as stdout.

The combined stream is then piped into grep.

If you want only stderr to be piped and keep stdout where it is, use the trick: /challenge/run 2>&1 >/dev/null | grep pwn.college.

Explanation: 2>&1 duplicates stderr to stdout; then >/dev/null redirects the (original) stdout to /dev/null, leaving the duplicated stderr on stdout to be piped.

Alternative (bash process substitution): /challenge/run 2> >(grep pwn.college >&2) — this runs grep on stderr only.

### What I learned

Combining streams is a common need — 2>&1 is the canonical way to merge stderr into stdout (order matters).

There are multiple ways to manipulate stderr and stdout — process substitution and redirect ordering let you be precise about which stream you pipe.

If capturing both streams, be mindful of interleaving: stderr and stdout can arrive in any order.

## 9. Filtering with grep -v
```
hacker@piping~filtering-with-grep-v:~$ /challenge/run | grep -v DECOY
pwn.college{EzcrLiJgZ8K-xgFhMI6n8ikoHxw.0FOxEzNxwSMwEzNzEzW}
hacker@piping~filtering-with-grep-v:~$ 
```

### Detailed steps

Use grep -v to exclude lines matching a pattern: /challenge/run | grep -v DECOY.

Verify that the unwanted DECOY lines are suppressed and the flag remains.

For more complex filtering, combine grep -v with grep -E or awk.

### What I learned

grep -v inverts the match — prints lines that do not match.

Use pipelines to perform staged filtering: cmd | grep -v DECOY | grep pwn.college.

sed and awk are powerful alternatives when you need to edit lines rather

## 10. Duplicating piped data with tee
```
hacker@piping~duplicating-piped-data-with-tee:~$ cat pwn
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "YnAvRkTw"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret YnAvRkTw | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{YnAvRkTwDZY7aZDhLivmych1HFF.QXxITO0wSMwEzNzEzW}
hacker@piping~duplicating-piped-data-with-tee:~$ 
```
### Steps:

First, you checked the usage of /challenge/pwn by running cat pwn.

It showed that the program required the argument --secret followed by the secret string YnAvRkTw.

You executed /challenge/pwn --secret YnAvRkTw and piped its output into /challenge/college.

Command: /challenge/pwn --secret YnAvRkTw | /challenge/college

The secret value was passed correctly, and /challenge/college confirmed the output by giving you the flag.

### What I Learned:

The tee command is useful when you want to duplicate piped output to multiple places.

Even though in this challenge you didn’t explicitly need tee, the lesson was about being able to split data streams in pipelines.

## 11. Process substitution for input
```
hacker@piping~process-substitution-for-input:~$ diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)
86a87
> pwn.college{QaifdLHuk41KYV7YB8CywJRbTKr.0lNwMDOxwSMwEzNzEzW}
hacker@piping~process-substitution-for-input:~$ 
```

### Steps:

You needed to compare two different outputs:

/challenge/print_decoys (only decoys).

/challenge/print_decoys_and_flag (decoys + flag).

To compare them, you used process substitution:

Command: diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)

diff showed you the line difference, revealing the flag.

### What I Learned:

Process substitution <(command) allows you to run a command and treat its output like a file input.

This makes it possible to use commands like diff without creating temporary files.

## 12. Writing to multiple programs
```
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) >(/challenge/planet)
This secret data must directly and simultaneously make it to /challenge/the and 
/challenge/planet. Don't try to copy-paste it; it changes too fast.
190092572972310229
Congratulations, you have duplicated data into the input of two programs! Here 
is your flag:
pwn.college{Ek8WpVJa78O6Jfp1Nf-6u08HpX2.QXwgDN1wSMwEzNzEzW}
hacker@piping~writing-to-multiple-programs:~$ 
```

### Steps:

The challenge required sending the same data stream from /challenge/hack to both /challenge/the and /challenge/planet.

Normally, pipes only send data in one direction. To duplicate it, you used tee.

You wrote:

/challenge/hack | tee >(/challenge/the) >(/challenge/planet)

tee duplicated the secret data and redirected it into two process substitutions simultaneously.

Both programs received the data, and you got the flag.

### What I Learned:

The tee command can send output to multiple places, not just files.

Combined with process substitution, it allows duplicating live data streams to multiple commands at once.


## 13. Split piping stderr and atdout
```
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack > >( /challenge/planet ) 2> >( /challenge/the )
Congratulations, you have learned a redirection technique that even experts 
struggle with! Here is your flag:
pwn.college{4ZYmORaxbaFpWCOWeXuVt_je7qW.QXxQDM2wSMwEzNzEzW}
hacker@piping~split-piping-stderr-and-stdout:~$ 
```

### Steps:

The challenge required you to handle stdout and stderr separately.

You redirected stdout with > into one process substitution and stderr with 2> into another.

The command you used was:

/challenge/hack > >( /challenge/planet ) 2> >( /challenge/the )

This meant:

Stdout goes into /challenge/planet.

Stderr goes into /challenge/the.

The redirection worked, and the flag was revealed.

### What I Learned:

> redirects standard output (file descriptor 1).

2> redirects standard error (file descriptor 2).

You can separately pipe stdout and stderr into different commands using process substitution.

## 14. Named pipes
```
hacker@piping~named-pipes:~$ mkfifo /tmp/flag_fifo
hacker@piping~named-pipes:~$ /challenge/run >/tmp/flag_fifo
You're successfully redirecting /challenge/run to a FIFO at /tmp/flag_fifo! 
Bash will now try to open the FIFO for writing, to pass it as the stdout of 
/challenge/run. Recall that operations on FIFOs will *block* until both the 
read side and the write side is open, so /challenge/run will not actually be 
launched until you start reading from the FIFO!

```
```
hacker@piping~named-pipes:~$ /challenge/run >/tmp/flag_fifo | cat /tmp/flag_fifo
You're successfully redirecting /challenge/run to a FIFO at /tmp/flag_fifo! 
Bash will now try to open the FIFO for writing, to pass it as the stdout of 
/challenge/run. Recall that operations on FIFOs will *block* until both the 
read side and the write side is open, so /challenge/run will not actually be 
launched until you start reading from the FIFO!
You've correctly redirected /challenge/run's stdout to a FIFO at 
/tmp/flag_fifo! Here is your flag:
You've correctly redirected /challenge/run's stdout to a FIFO at 
/tmp/flag_fifo! Here is your flag:
pwn.college{AdgPeX_CiELWX6dQ3BUmTsIBw9E.01MzMDOxwSMwEzNzEzW}
pwn.college{AdgPeX_CiELWX6dQ3BUmTsIBw9E.01MzMDOxwSMwEzNzEzW}
hacker@piping~named-pipes:~$ 
```

### Steps:

You created a named pipe (FIFO) using:

mkfifo /tmp/flag_fifo

You redirected the output of /challenge/run into this FIFO:

/challenge/run >/tmp/flag_fifo

At this point, it blocked because FIFOs require both a reader and a writer.

To solve the blocking issue, you used a pipeline where /challenge/run wrote to the FIFO and cat read from it:

/challenge/run >/tmp/flag_fifo | cat /tmp/flag_fifo

This ensured both sides of the FIFO were active, so the program ran and printed the flag.

### What I Learned:

A FIFO (named pipe) is like a special file used for inter-process communication.

Writing to a FIFO blocks until another process opens it for reading.

This technique allows connecting processes in more flexible ways than regular pipes.

