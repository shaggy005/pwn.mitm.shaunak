# Pondering Path
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
## 3. FInding Commands
```
hacker@path~finding-commands:~$ dir="$(dirname "$(readlink -f "$(which win)")")"
hacker@path~finding-commands:~$ cat "$dir/flag"
pwn.college{cZEYFqHh5dbEYrV_F6uzKU0OiXT.01NzEzNxwSMwEzNzEzW}
```
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
## 5. Hijacking Commands
```

```
