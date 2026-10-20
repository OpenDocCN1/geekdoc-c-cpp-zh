41. Store the man pages for bash, sh, and csh in a file called shell_man_pages. Use the gzip command to compress with different levels of compression. Show your work and identify the command that does the maximum compression, along with the compression ratio.

42. Use the base64 and openssl commands to encode /bin/bash and place encoded content in the my_bash file in your current directory. Then, use base64 and openssl to decode the encoded file. Finally, use the shasum command to confirm that /bin/bash and my_bash are identical.

43. How many encryption algorithms does the mcrypt command support? What command did you use to obtain your answer? Create the memo1 file discussed in Section 7.9 and encrypt it using the md5 and crc32 algorithms. Which of the two exhibits higher space efficiency? Show your work.

# Advanced Questions and Problems

44. Consider the persons file contains the following data with each line containing a person's last name and his/her age. Give the command to sort persons based on age, numerically.

```
$ cat persons
Linus,47
Judy,20
Maham,25
Adelson,85
Amy,38
Jacobson,25
$
```

45. What is the difference between the outputs of the following commands:
a. find ~
b. find ~ -L

46. What is the difference between the outputs of the following commands:
c. find ~ -name 'apple'
d. find ~ -iname 'apple'
e. find ~ -name 'apple' -type f
f. find ~ -name 'apple' -type d
g. find ~ | grep 'apple'

47. Give the command to display the names of files in your home directory that have been modified during the past 24 hours.

48. The executable files for the commands used normally by the superuser are found in /sbin and /usr/sbin directories. Give the command that displays pathnames for all the files in these directories that are executable but not readable.

49. Give the command that display the total number of files under your system's file system hierarchy owned by root, excluding files in the directories that you cannot open. How many such files exist on your system?

50. Give the command that displays the number of directories that you cannot search in your file system hierarchy. How many such directories do you have on your system? Show the command and its output on your Linux system.

51. Give the command to locate all C program files in or below your home directory, but limit subdirectory traversal to three levels beneath the home directory.

52. What do the regular expressions ^$, ^#*, and ^A* match?

53. What would be the regular expression to search for a string that
a. starts with letter M,
b. is the first word on a line,