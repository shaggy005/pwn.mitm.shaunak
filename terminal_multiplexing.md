# Terminal Multiplexing
## 1. Launching Screen
```
hacker@terminal-multiplexing~launching-screen:~$ screen
    Screen version 5.0.1 (build on 2025-05-15 15:05:07) 
Copyright (c) 2025 Alexander Naumov
Copyright (c) 2018-2024 Alexander Naumov, Amadeusz Slawinski
Copyright (c) 2015-2017 Juergen Weigert, Alexander Naumov, Amadeusz Slawinski
Copyright (c) 2010-2014 Juergen Weigert, Sadrul Habib Chowdhury
Copyright (c) 2008-2009 Juergen Weigert, Michael Schroeder, Micah Cowan, Sadrul
Habib Chowdhury
Copyright (c) 1993-2007 Juergen Weigert, Michael Schroeder
Copyright (c) 1987 Oliver Laumann

This program is free software; you can redistribute it and/or modify it under the
terms of the GNU General Public License as published by the Free Software
Foundation; either version 3, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this
program (see the file COPYING); if not, see https://www.gnu.org/licenses/, or
contact Free Software Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston,
MA  02111-1301  USA.

Send bugreports, fixes, enhancements, t-shirts, money, beer & pizza to
screen-devel@gnu.org
Congratulations! You're inside a screen session!
Here's your flag:
pwn.college{UlSC0XLenTooRtIRU6Wnq2H6nwm.0VN4IDOxwSMwEzNzEzW}
hacker@terminal-multiplexing~launching-screen:~$
```
### Steps

I started a screen session to create a persistent terminal environment. After entering the session, I confirmed I was inside a screen instance and the challenge printed the flag from within that session.

### What I Learned

I learned how to launch and enter a screen session, which gives me a detachable, persistent terminal that continues running even if I disconnect. This is useful for long-running tasks and for keeping programs alive between logins.

### References
man screen

## 2. Detaching and attaching
```
screen
/challenge/run
screen -r
hacker@terminal-multiplexing~detaching-and-attaching:~$ echo Yes! Flag is: pwn.college{Ex4JvfLnR91EVfsg9zWOg_D1E1x.0lN4IDOxwSMwEzNzEzW}
Yes! Flag is: pwn.college{Ex4JvfLnR91EVfsg9zWOg_D1E1x.0lN4IDOxwSMwEzNzEzW}
hacker@terminal-multiplexing~detaching-and-attaching:~$
```
### Steps

I launched a screen session and then detached from it so the session continued running in the background. Later I reattached to the same session and observed the running program’s output, which included the flag.

### What I Learned

I learned how to detach from a screen session to leave processes running and how to reattach later to regain interactive control. This reinforced the workflow for maintaining persistent interactive workspaces.

### References

GNU Screen user manual (detaching/attaching)

Tutorials on persistent shells with screen

yeah my overconfident ass had to watch yt tutorials to do ts this time

## 3. Finding sessions
```
hacker@terminal-multiplexing~finding-sessions:~$ screen -ls There are screens on: 158.pts-0.terminal-multiplexing~launching-screen (Remote or dead)
147.pts-0.terminal-multiplexing~detaching-and-attaching (Remote or dead)
144.session_edcad0a4776b591d (Remote or dead)
147.session_ffb3d04b28b8a1d0 (Remote or dead)
150.session_72f18355bb971ed1 (Remote or dead)
144.session_10dc83fcb6364c8d (Detached)
147.session_0fe960d9a41d6481 (Detached)
150.session_2d526b417d9827c9 (Detached)
8 Sockets in /home/hacker/.screen.
screen -r 144.session_10dc83fcb6364c8d
hacker@terminal-multiplexing~finding-sessions:~$  echo 'Congratulations! You found the right session!'
Congratulations! You found the right session!
hacker@terminal-multiplexing~finding-sessions:~$  echo pwn.college{kGfbBfIPTa1yFuV5wPbITfaVUPc.01N4IDOxwSMwEzNzEzW}
pwn.college{kGfbBfIPTa1yFuV5wPbITfaVUPc.01N4IDOxwSMwEzNzEzW}
hacker@terminal-multiplexing~finding-sessions:~$ /challenge/run
```
### Steps

I listed active screen sessions to discover detached or running sockets. I identified the correct session by name/ID, attached to it, and located the message that revealed the flag.

### What I Learned

I learned how to enumerate screen sockets and sessions, how to interpret the listing output, and how to pick and attach a specific session. This is valuable when multiple sessions exist on the same host.

### References

man screen (session management)

## 4. Switching windows
```
hacker@terminal-multiplexing~switching-windows:~$ screen -ls
There are screens on:
        158.pts-0.terminal-multiplexing~launching-screen        (Remote or dead)
        147.pts-0.terminal-multiplexing~detaching-and-attaching (Remote or dead)
        144.session_edcad0a4776b591d    (Remote or dead)
        147.session_ffb3d04b28b8a1d0    (Remote or dead)
        150.session_72f18355bb971ed1    (Remote or dead)
        144.session_10dc83fcb6364c8d    (Remote or dead)
        147.session_0fe960d9a41d6481    (Remote or dead)
        150.session_2d526b417d9827c9    (Remote or dead)
        135.challenge_session   (Detached)
9 Sockets in /home/hacker/.screen.
hacker@terminal-multiplexing~switching-windows:~$ screen -r 135.challenge_session
 cat <<MSG
Welcome to the window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-A 0 to switch to window 0!
MSG
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Welcome to the window switching challenge!
> You are currently in window 1.
> The flag is hidden in window 0.
> Use Ctrl-A 0 to switch to window 0!
> MSG
Welcome to the window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-A 0 to switch to window 0!
hacker@terminal-multiplexing~switching-windows:~$
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{ULLKh62zul4iajWLZzSFAK6UN_w.0FO4IDOxwSMwEzNzEzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{ULLKh62zul4iajWLZzSFAK6UN_w.0FO4IDOxwSMwEzNzEzW}
hacker@terminal-multiplexing~switching-windows:~$ 
```
### Steps

Inside a screen session, I switched between numbered windows to locate content hidden in a different window. I followed the prompt to switch to the indicated window and found the flag printed there.

### What I Learned
I learned that terminal multiplexers support multiple windows inside a session and that each window can contain separate processes or shells. Mastering window switching (by index) helps to organize work and find outputs that are intentionally placed in other windows.

### References

GNU Screen window management docs

Multiplexing best practices and window navigation tips
## 5. Detatching and Attatching (tmux)
```
tmux
ctrl+b d
/challenge/run
tmux attach
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$  echo Congratulations, here is your flag: pwn.college{YmW-yZSTusRIUNck_85X2RHT1Lv.0VO4IDOxwSMwEzNzEzW}
Congratulations, here is your flag: pwn.college{YmW-yZSTusRIUNck_85X2RHT1Lv.0VO4IDOxwSMwEzNzEzW}
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ 
```
### Steps

I used tmux to create a session, detached from it to allow the program to keep running, and then reattached to the session to inspect the output. The challenge printed the flag after I reattached.

### What I Learned

I learned the equivalent tmux workflow for creating persistent sessions, detaching, and attaching. While conceptually similar to screen, tmux has different default keybindings and configuration options; both are valuable tools for session persistence.

### References

man tmux
## 6. 
```
tmux ls
tmux attach
ctrl+b 0
 cat <<MSG
Welcome to the tmux window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-B 0 to switch to window 0!
MSG
hacker@terminal-multiplexing~switching-windows-tmux:~$  cat <<MSG
> Welcome to the tmux window switching challenge!
> You are currently in window 1.
> The flag is hidden in window 0.
> Use Ctrl-B 0 to switch to window 0!
> MSG
Welcome to the tmux window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-B 0 to switch to window 0!
hacker@terminal-multiplexing~switching-windows-tmux:~$
hacker@terminal-multiplexing~switching-windows-tmux:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{85E3k2jq5hw6unxRvuHZRsAAudV.0FM5IDOxwSMwEzNzEzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{85E3k2jq5hw6unxRvuHZRsAAudV.0FM5IDOxwSMwEzNzEzW}
hacker@terminal-multiplexing~switching-windows-tmux:~$ 
```
### Steps

Within a tmux session I enumerated windows and used the appropriate key combo to switch to the target window. The flag was hidden in a different window and was revealed once I switched to it.

### What I Learned

I learned how tmux manages multiple windows within a session and how to navigate between them using tmux keybindings. This reinforced the general multiplexing concept that sessions can host multiple independent, switchable windows.

### References

Tmux window management documentation

Comparisons of screen vs tmux for window handling
