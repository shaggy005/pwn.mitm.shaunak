# 1. Translating Charecters
```
hacker@data~translating-characters:~$ /challenge/run | tr 'A-Za-z' 'a-zA-Z'
yOUR CASE-SWAPPED FLAG:
pwn.college{EBbB4I6pC9z10Wzs20YFkpG6YSF.01MxEzNxwSMwEzNzEzW}

hacker@data~translating-characters:~$
```
# 2. Deleting characters
```
hacker@data~deleting-characters:~$ /challenge/run | tr -d '^%'
Your character-stuffed flag:
pwn.college{kdBA6mmgYuhQvY4ylwNsMo2oGa4.0FNxEzNxwSMwEzNzEzW}
hacker@data~deleting-characters:~$ 
```
# 3. Deleting newlines
```
hacker@data~deleting-newlines:~$ /challenge/run | tr -d '\n'
Your line-split flag: pwn.college{s2xts6Byeg7nZLBjAsrAWTD5QYs.0VNxEzNxwSMwEzNzEzW}
hacker@data~deleting-newlines:~$ 
```
# 4. Extracting the first lines with head
```
hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n 7 | /challenge/college
Congratulations, you piped the right codes!
pwn.college{M617O87zN5aeaoOfwsbZ2zsRJqC.0lNxEzNxwSMwEzNzEzW}
hacker@data~extracting-the-first-lines-with-head:~$ 
```
# 5. Extracting specific sections of text
```
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d ' ' -f 2 | tr -d '\n'
pwn.college{oZRld4vyo-Mr1WzZQon_gCCoanI.01NxEzNxwSMwEzNzEzW}
hacker@data~extracting-specific-sections-of-text:~$ 
```
# 6. Sorting Data
```
hacker@data~sorting-data:~$ sort /challenge/flags.txt | tail -n 1
pwn.college{E1lgSb6FSe9-NH2U4bVKnjefw2Y.0FM0MDOxwSMwEzNzEzW}
hacker@data~sorting-data:~$ 

```
