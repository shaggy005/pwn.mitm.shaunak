
# Comprehending Commands

This writeup documents my solutions for various Linux command exercises in pwn.college.

---

## 1. cat: Not the Pet, But the Command

**Steps:**  
Use `cat` to display the contents of a file named `flag`.

**Terminal Snapshot:**
```bash
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{QGBz379w8crgZx3NZlOjQJ3aihS.QXxcTN0wSMwEzNzEzW}
hacker@commands~cat-not-the-pet-but-the-command:~$ 
```

**What I Learned:**  
- `cat` reads the contents of files.
- Useful for quickly viewing files from the terminal.

---

## 2. Catting Absolute Paths

**Steps:**  
Access a file using its absolute path without relying on the current directory.

**Terminal Snapshot:**
```bash
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{Uj3pkpAM-hk_pM5wdeGibA5Otp2.QX5ETO0wSMwEzNzEzW}
hacker@commands~catting-absolute-paths:~$ 
```

**What I Learned:**  
- Absolute paths start from `/` and can be accessed from anywhere.
- Critical when `cd` is not allowed.

---

## 3. More Catting Practice

**Steps:**  
Retrieve a flag from a hidden system directory using absolute path.

**Terminal Snapshot:**
```bash
hacker@commands~more-catting-practice:~$ cat /usr/lib/systemd/flag
pwn.college{E8RpnsS7SWETm6xmWG1Wm2K6XoO.QXwITO0wSMwEzNzEzW}
hacker@commands~more-catting-practice:~$ 
```

**What I Learned:**  
- `cat` works on any file if you know the full path.
- Hidden system directories may contain flags.

---

## 4. Grepping for a Needle in a Haystack

**Steps:**  
Search a file for a specific pattern using `grep`.

**Terminal Snapshot:**
```bash
Connected!
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep 'pwn\.college' /challenge/data.txt
pwn.college{o8zdKXC1KIwB5AsBZMH0bQZ1xCv.QX3EDO0wSMwEzNzEzW}

hacker@commands~grepping-for-a-needle-in-a-haystack:~$ 
```

**What I Learned:**  
- `grep` searches for matching patterns in files.
- Escape special characters like `.` in the pattern.

---

## 5. Comparing Files

**Steps:**  
Compare two files to spot differences using `diff`.

**Terminal Snapshot:**
```bash
hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
11a12
> pwn.college{cXUc7sd_FzbagWT9AcUWlV19bF2.01MwMDOxwSMwEzNzEzW}
hacker@commands~comparing-files:~$ 
```

**What I Learned:**  
- `diff` highlights differences line by line.
- Useful for spotting hidden flags in slightly different files.

---

## 6. Listing Files

**Steps:**  
List files in a directory and check the contents of interesting files.

**Terminal Snapshot:**
```bash
hacker@commands~listing-files:~$ ls /challenge
16634-renamed-run-26078  DESCRIPTION.md
hacker@commands~listing-files:~$ cat /challenge/16634-renamed-run-26078
#!/opt/pwn.college/bash
echo "Yahaha, you found me! Here is your flag:"
cat /flag
hacker@commands~listing-files:~$ /challenge/16634-renamed-run-26078
Yahaha, you found me! Here is your flag:
pwn.college{MAXNJsZZSZY07JGMpWJ4xMCNcS7.QX4IDO0wSMwEzNzEzW}
hacker@commands~listing-files:~$ 
```

**What I Learned:**  
- `ls` lists directory contents.
- Running scripts can reveal hidden flags.

---

## 7. Touching Files

**Steps:**  
Create empty files and trigger a challenge script.

**Terminal Snapshot:**
```bash
hacker@commands~touching-files:~$ touch /tmp/pwn /tmp/college
hacker@commands~touching-files:~$ /challenge/run
Success! Here is your flag:
pwn.college{gpa11VS4HeAllngyl1oya5wkybx.QXwMDO0wSMwEzNzEzW}
hacker@commands~touching-files:~$ 
```

**What I Learned:**  
- `touch` creates empty files.
- Some scripts require files to exist to trigger flags.

---

## 8. Removing Files

**Steps:**  
Delete a file using `rm` and verify with the challenge checker.

**Terminal Snapshot:**
```bash
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{APeIN-j0uRreJx7oAWzEzh3ePkl.QX2kDM1wSMwEzNzEzW}
hacker@commands~removing-files:~$ 
```

**What I Learned:**  
- `rm` deletes files permanently.
- Removing specific files can be part of a challenge.

---

## 9. Moving Files

**Steps:**  
Move a file to a new location using `mv` and verify the move.

**Terminal Snapshot:**
```bash
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{c73-Cm4uNLAOIIUgzCQ5Cyh4z7R.0VOxEzNxwSMwEzNzEzW}
hacker@commands~moving-files:~$ 
```

**What I Learned:**  
- `mv` moves or renames files.
- Correct paths are crucial.

---

## 10. Hidden Files

**Steps:**  
Reveal hidden files using `ls -a` and read hidden flags with `cat`.

**Terminal Snapshot:**
```bash
hacker@commands~hidden-files:~$ cd /.
ls -a
.                     bin        etc    lib64   nix   run   tmp
..                    boot       home   libx32  opt   sbin  usr
.dockerenv            challenge  lib    media  proc  srv   var
.flag-23135706724664  dev        lib32  mnt    root  sys
hacker@commands~hidden-files:/$ cat /.flag-23135706724664
pwn.college{4tPVMiWLlCs2BAqodyvFTef07Y3.QXwUDO0wSMwEzNzEzW}
hacker@commands~hidden-files:/$ 
```

**What I Learned:**  
- Hidden files start with a `.`.
- `ls -a` lists all files, including hidden ones.

---

## 11. An Epic Filesystem Quest

**Steps:**  
Follow clues across directories using absolute paths. Avoid `cd` for trapped clues and use `ls` and `cat` to read them.

**Terminal Snapshot:**
```bash
hacker@commands~an-epic-filesystem-quest:~$ cd /.
hacker@commands~an-epic-filesystem-quest:/$ ls -a
.           INFO  challenge  flag  lib32   media  opt   run   sys  var
..          bin   dev        home  lib64   mnt    proc  sbin  tmp
.dockerenv  boot  etc        lib   libx32  nix    root  srv   usr
hacker@commands~an-epic-filesystem-quest:/$ cd /INFO
bash: cd: /INFO: Not a directory
hacker@commands~an-epic-filesystem-quest:/$ cat INFO
Congratulations, you found the clue!
The next clue is in: /usr/lib/python3/dist-packages/scipy/spatial/transform/tests

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/$ cat /usr/lib/python3/dist-packages/scipy/spatial/transform/tests
cat: /usr/lib/python3/dist-packages/scipy/spatial/transform/tests: Is a directory
hacker@commands~an-epic-filesystem-quest:/$ ls /usr/lib/python3/dist-packages/scipy/spatial/transform/tests
MEMO-TRAPPED  __pycache__       test_rotation_spline.py
__init__.py   test_rotation.py
hacker@commands~an-epic-filesystem-quest:/$ cat /usr/lib/python3/dist-packages/scipy/spatial/transform/tests/MEMO-TRAPPED
Congratulations, you found the clue!
The next clue is in: /opt/linux/linux-5.4/drivers/usb/c67x00
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/drivers/usb/c67x00$ ls
Makefile  c67x00-drv.c  c67x00-hcd.h     c67x00-sched.c
WHISPER   c67x00-hcd.c  c67x00-ll-hpi.c  c67x00.h
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/drivers/usb/c67x00$ cat WHISPER
Yahaha, you found me!
The next clue is in: /usr/local/lib/python3.8/dist-packages/fastecdsa/__pycache__

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/drivers/usb/c67x00$ cd /usr/local/lib/python3.8/dist-packages/fastecdsa/__pycache__
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/fastecdsa/__pycache__$ ls
HINT                     benchmark.cpython-38.pyc  ecdsa.cpython-38.pyc  point.cpython-38.pyc
__init__.cpython-38.pyc  curve.cpython-38.pyc      keys.cpython-38.pyc   util.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/fastecdsa/__pycache__$ cat HINT
Congratulations, you found the clue!
The next clue is in: /usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX-Web/Normal/Italic

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/fastecdsa/__pycache__$ cd /usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX-Web/Normal/Italic
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX-Web/Normal/Italic$ ls
Main.js  SECRET
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX-Web/Normal/Italic$ cat SECRET
Congratulations, you found the clue!
The next clue is in: /usr/share/doc/libatomic-ops-dev

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX-Web/Normal/Italic$ ls /usr/share/doc/libatomic-ops-dev
AUTHORS           README.Debian          README_malloc.txt  README_win32.txt     copyright
EVIDENCE-TRAPPED  README_details.txt.gz  README_stack.txt   changelog.Debian.gz
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX-Web/Normal/Italic$ cat /usr/share/doc/libatomic-ops-dev/EVIDENCE-TRAPPED
Congratulations, you found the clue!
The next clue is in: /opt/pwndbg/.venv/lib/python3.8/site-packages/setuptools/_vendor/importlib_resources/__pycache__
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX-Web/Normal/Italic$ ls /opt/pwndbg/.venv/lib/python3.8/site-packages/setuptools/_vendor/importlib_resources/__pycache__
DOSSIER                   _common.cpython-38.pyc     _legacy.cpython-38.pyc  simple.cpython-38.pyc
__init__.cpython-38.pyc   _compat.cpython-38.pyc     abc.cpython-38.pyc
_adapters.cpython-38.pyc  _itertools.cpython-38.pyc  readers.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX-Web/Normal/Italic$ cat /opt/pwndbg/.venv/lib/python3.8/site-packages/setuptools/_vendor/importlib_resources/__pycache__/DOSSIER
Lucky listing!
The next clue is in: /usr/share/javascript/mathjax/unpacked/jax/input

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/input$ ls
AsciiMath  MathML  SNIPPET  TeX
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/input$ cat SNIPPET
Yahaha, you found me!
The next clue is in: /usr/share/racket/pkgs/drracket/setup

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/input$ ls /usr/share/racket/pkgs/drracket/setup -a
.   .NOTE     info.rkt               plt-installer-unit.rkt  plt-installer.scrbl
..  compiled  plt-installer-sig.rkt  plt-installer.rkt
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/input$ cat /usr/share/racket/pkgs/drracket/setup/.NOTE
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{0nQdbY-MrzzNoncQwyRNTX5s6Tl.QX5IDO0wSMwEzNzEzW}
```

**What I Learned:**  
- Some clues require `cd` to access delayed content.  
- Hidden files often start with a `.` and require `ls -a` to reveal.  
- Combining `ls` and `cat` carefully can help navigate complex filesystem challenges.

---
## 12. Making Directories

**Steps:**  
Create directories with `mkdir`, add files, and trigger the challenge script.

**Terminal Snapshot:**
```bash
hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ cd /tmp/pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ /challenge/run
Success! Here is your flag:
pwn.college{8B5i_H3h5Xq1UT_yCtkGNTFByrk.QXxMDO0wSMwEzNzEzW}
hacker@commands~making-directories:/tmp/pwn$ 
```

**What I Learned:**  
- `mkdir` creates new directories.  
- Files inside directories can trigger scripts or challenges.

---

## 13. Finding Files

**Steps:**  
Search the filesystem for files named `flag` using `find`, then read them with `cat`.

**Terminal Snapshot:**
```bash
hacker@commands~finding-files:~$ find / -name flag
find: ‘/tmp/tmp.TpSOPGOVKK’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/share/vim/vim81/pack/dist/opt/termdebug/flag
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/mysql-files’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/mysql’: Permission denied
find: ‘/var/lib/mysql-keyring’: Permission denied
find: ‘/var/lib/php/sessions’: Permission denied
find: ‘/var/log/private’: Permission denied
find: ‘/var/log/apache2’: Permission denied
find: ‘/var/log/mysql’: Permission denied
find: ‘/run/mysqld’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/root’: Permission denied
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
find: ‘/proc/tty/driver’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/7/task/7/fd’: Permission denied
find: ‘/proc/7/task/7/fdinfo’: Permission denied
find: ‘/proc/7/task/7/ns’: Permission denied
find: ‘/proc/7/fd’: Permission denied
find: ‘/proc/7/map_files’: Permission denied
find: ‘/proc/7/fdinfo’: Permission denied
find: ‘/proc/7/ns’: Permission denied
/nix/store/ka6xbd6z6wj5d6frl7ym4nzfc6p2wkdx-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/f31j0igg7ms3yrj5gm3cm76bjcmdl8w5-python3.12-pwntools-4.13.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/7ns27apnvn4qj4q5c82x0z1lzixrz47p-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/5z3sjp9r463i3siif58hq5wj5jmy5m98-python3.12-pwntools-4.13.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/n6vb30rd7kkwjj595pgm0dmsmfaqi6i5-rizin-0.7.3/share/rizin/flag
/nix/store/5n5lp1m8gilgrsriv1f2z0jdjk50ypcn-rizin-0.7.3/share/rizin/flag
/nix/store/bnlabj2vsbljhp597ir29l51nrqhm89w-rizin-0.7.4/share/rizin/flag
/nix/store/s8b49lb0pqwvw0c6kgjbxdwxcv2bp0x4-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/8qvj9mzdq2qxgjigw4ysqgbkcx1zi80y-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/1hyxipvwpdpcxw90l5pq1nvd6s6jdi5m-python3.12-pwntools-4.14.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/dz2qxywk6d8hc1gkarpwbhyxb50sh2ak-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag
hacker@commands~finding-files:~$ cat /usr/share/vim/vim81/pack/dist/opt/termdebug/flag
pwn.college{Mw8i6qUXebBUHV2cL6uDx2LQxpp.QXyMDO0wSMwEzNzEzW}
```

**What I Learned:**  
- `find / -name <filename>` recursively searches the filesystem.  
- Many directories are restricted (Permission denied).  
- Combining `find` with `cat` lets you locate and read flags quickly.  
