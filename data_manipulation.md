# Data Manipulation
## 1. Translating Characters
```
hacker@data~translating-characters:~$ /challenge/run | tr 'A-Za-z' 'a-zA-Z'
yOUR CASE-SWAPPED FLAG:
pwn.college{EBbB4I6pC9z10Wzs20YFkpG6YSF.01MxEzNxwSMwEzNzEzW}

hacker@data~translating-characters:~$
```
### Steps

I first ran the challenge to see the output. The task required me to swap the case of all letters — changing uppercase to lowercase and lowercase to uppercase. I used the tr command to perform this translation by mapping one range of characters to another. After running it with the correct parameters, the output displayed the case-swapped flag.

### What I Learned

I learned how the tr command can be used to translate or replace specific characters in text streams. I understood that it works by taking two sets of characters and mapping them one-to-one. This taught me how to perform simple but powerful text transformations directly from the terminal.

### References
man tr

## 2. Deleting characters
```
hacker@data~deleting-characters:~$ /challenge/run | tr -d '^%'
Your character-stuffed flag:
pwn.college{kdBA6mmgYuhQvY4ylwNsMo2oGa4.0FNxEzNxwSMwEzNzEzW}
hacker@data~deleting-characters:~$
```
### Steps

When I ran the challenge, the output included unwanted symbols mixed in with the flag. To clean it up, I used the tr command with the delete option to remove specific characters. After deleting the unnecessary ones, the flag appeared clearly.

### What I Learned

I learned that the delete option in tr can remove any specified characters from the input stream. It’s a quick way to clean text or filter out unwanted symbols. I also learned that multiple characters can be deleted at once by specifying them together.

### References

man tr

## 3. Deleting newlines
```
hacker@data~deleting-newlines:~$ /challenge/run | tr -d '\n'
Your line-split flag: pwn.college{s2xts6Byeg7nZLBjAsrAWTD5QYs.0VNxEzNxwSMwEzNzEzW}
hacker@data~deleting-newlines:~$ 
```
### Steps

The flag output for this challenge was split across several lines. I needed to merge everything into a single continuous line. I used the translation command to delete newline characters, effectively joining all lines together. The final result was the complete flag in one line.

### What I Learned

I learned that newline characters (\n) can be treated like any other character and removed using the tr command. This is useful for flattening multiline text into one line, especially when processing output that spans several lines. It helped me understand text stream manipulation better.

### References

man tr

## 4. Extracting the first lines with head
```
hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n 7 | /challenge/college
Congratulations, you piped the right codes!
pwn.college{M617O87zN5aeaoOfwsbZ2zsRJqC.0lNxEzNxwSMwEzNzEzW}
hacker@data~extracting-the-first-lines-with-head:~$ 
```
### Steps

The challenge output contained multiple lines of data, but I only needed the first few. I used the head command to extract the first seven lines and piped them into another command to verify the result. Once done, it confirmed that the correct portion of data was used.

### What I Learned

I learned how the head command can be used to extract a specific number of lines from the beginning of a text stream. I also understood the importance of pipes in connecting multiple commands together to form data processing chains. This showed me how Unix commands can be combined efficiently.

### References

man head
## 5. Extracting specific sections of text
```
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d ' ' -f 2 | tr -d '\n'
pwn.college{oZRld4vyo-Mr1WzZQon_gCCoanI.01NxEzNxwSMwEzNzEzW}
hacker@data~extracting-specific-sections-of-text:~$ 
```
### Steps

The output for this challenge consisted of multiple words separated by spaces, and I needed to pick only the second word from each line. I used the cut command to extract that specific field. After that, I removed unwanted newlines to join everything neatly, which revealed the flag.

### What I Learned

I learned how to use the cut command to extract specific fields or columns from structured text data. The delimiter and field options allow precise control over which part of the text to select. Combining it with other text tools taught me how to manipulate data streams more effectively.

### References

man cut
## 6. Sorting Data
```
hacker@data~sorting-data:~$ sort /challenge/flags.txt | tail -n 1
pwn.college{E1lgSb6FSe9-NH2U4bVKnjefw2Y.0FM0MDOxwSMwEzNzEzW}
hacker@data~sorting-data:~$ 

```
### Steps

In this challenge, I was given a file with multiple lines of text. My goal was to find the alphabetically last one. I used the sort command to arrange the lines, then selected the final entry to get the correct flag. This combination worked as expected.

### What I Learned

I learned that the sort command arranges lines of text in lexicographical order by default. I also saw how combining sort with another command like tail can help isolate specific entries based on order. This taught me how to use sorting for quick text analysis and extraction tasks.

### References

man sort and man tail
