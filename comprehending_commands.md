1. cat: Not the Pet, But the Command

Steps:

Use cat to display the contents of a file named flag.

Terminal Snapshot:

hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{QGBz379w8crgZx3NZlOjQJ3aihS.QXxcTN0wSMwEzNzEzW}
hacker@commands~cat-not-the-pet-but-the-command:~$ 


What I Learned:

cat is used to read the contents of files.

It’s useful for quickly viewing files from the terminal.

2. Catting Absolute Paths

Steps:

Access a file using its absolute path without relying on the current directory.

Terminal Snapshot:

hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{Uj3pkpAM-hk_pM5wdeGibA5Otp2.QX5ETO0wSMwEzNzEzW}
hacker@commands~catting-absolute-paths:~$ 


What I Learned:

Absolute paths start with / and work from anywhere in the filesystem.

This is critical when cd is not allowed.

3. More Catting Practice

Steps:

Retrieve a flag from a hidden system directory using absolute path.

Terminal Snapshot:

hacker@commands~more-catting-practice:~$ cat /usr/lib/systemd/flag
pwn.college{E8RpnsS7SWETm6xmWG1Wm2K6XoO.QXwITO0wSMwEzNzEzW}
hacker@commands~more-catting-practice:~$ 


What I Learned:

cat works on any file if the full path is known.

Knowing hidden system directories is useful for finding flags.

4. Grepping for a Needle in a Haystack

Steps:

Search a file for a specific pattern using grep.

Terminal Snapshot:

Connected!
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep 'pwn\.college' /challenge/data.txt
pwn.college{o8zdKXC1KIwB5AsBZMH0bQZ1xCv.QX3EDO0wSMwEzNzEzW}

hacker@commands~grepping-for-a-needle-in-a-haystack:~$ 


What I Learned:

grep searches for matching patterns in files.

Escape special characters in the search pattern when necessary.

5. Comparing Files

Steps:

Compare two files to spot differences using diff.

Terminal Snapshot:

hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
11a12
> pwn.college{cXUc7sd_FzbagWT9AcUWlV19bF2.01MwMDOxwSMwEzNzEzW}
hacker@commands~comparing-files:~$ 


What I Learned:

diff shows line-by-line differences between files.

Useful for spotting flags hidden in slightly different copies.

6. Listing Files

Steps:

List files in a directory and check the contents of interesting files.

Terminal Snapshot:

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


What I Learned:

ls lists directory contents.

Running scripts can reveal hidden flags.

7. Touching Files

Steps:

Create empty files and trigger a challenge script.

Terminal Snapshot:

hacker@commands~touching-files:~$ touch /tmp/pwn /tmp/college
hacker@commands~touching-files:~$ /challenge/run
Success! Here is your flag:
pwn.college{gpa11VS4HeAllngyl1oya5wkybx.QXwMDO0wSMwEzNzEzW}
hacker@commands~touching-files:~$ 


What I Learned:

touch creates empty files quickly.

Some challenges require certain files to exist.

8. Removing Files

Steps:

Delete a file using rm and verify with the challenge checker.

Terminal Snapshot:

hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{APeIN-j0uRreJx7oAWzEzh3ePkl.QX2kDM1wSMwEzNzEzW}
hacker@commands~removing-files:~$ 


What I Learned:

rm deletes files permanently.

Removing specific files can be part of a puzzle.

9. Moving Files

Steps:

Move a file to a new location with mv and verify the move.

Terminal Snapshot:

hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{c73-Cm4uNLAOIIUgzCQ5Cyh4z7R.0VOxEzNxwSMwEzNzEzW}
hacker@commands~moving-files:~$ 


What I Learned:

mv moves or renames files.

Correct paths are crucial for challenge success.

10. Hidden Files

Steps:

Reveal hidden files with ls -a and read hidden flags with cat.

Terminal Snapshot:

hacker@commands~hidden-files:~$ cd /.
ls -a
.                     bin        etc    lib64   nix   run   tmp
..                    boot       home   libx32  opt   sbin  usr
.dockerenv            challenge  lib    media  proc  srv   var
.flag-23135706724664  dev        lib32  mnt    root  sys
hacker@commands~hidden-files:/$ cat /.flag-23135706724664
pwn.college{4tPVMiWLlCs2BAqodyvFTef07Y3.QXwUDO0wSMwEzNzEzW}
hacker@commands~hidden-files:/$ 


What I Learned:

Hidden files start with ..

ls -a shows all files in a directory, including hidden ones.

11. An Epic Filesystem Quest

Steps:

Follow a multi-step filesystem quest.

Read clues without using cd when warned.

Use ls and cat to explore files and directories.

Terminal Snapshot:

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
...
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
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/input$ 


What I Learned:

Some clues are trapped or hidden.

Understanding filesystem structure is critical.

Combine ls and cat carefully to retrieve flags without triggering traps.

12. Making Directories

Steps:

Create directories with mkdir.

Add files and trigger the challenge script.

Terminal Snapshot:

hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ cd /tmp/pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ /challenge/run
Success! Here is your flag:
pwn.college{8B5i_H3h5Xq1UT_yCtkGNTFByrk.QXxMDO0wSMwEzNzEzW}
hacker@commands~making-directories:/tmp/pwn$ 


What I Learned:

mkdir creates new directories.

Files in directories can be part of challenge logic.

13. Finding Files

Steps:

Search the filesystem for files named flag using find.

Read the flag with cat.

Terminal Snapshot:

hacker@commands~finding-files:~$ find / -name flag
find: ‘/tmp/tmp.TpSOPGOVKK’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/share/vim/vim81/pack/dist/opt/termdebug/flag
...
hacker@commands~finding-files:~$ cat /usr/share/vim/vim81/pack/dist/opt/termdebug/flag
pwn.college{Mw8i6qUXebBUHV2cL6uDx2LQxpp.QXyMDO0wSMwEzNzEzW}
hacker@commands~finding-files:~$ 


What I Learned:

find searches recursively and helps locate hidden or system files.

Combine with cat to read contents of files quickly.
