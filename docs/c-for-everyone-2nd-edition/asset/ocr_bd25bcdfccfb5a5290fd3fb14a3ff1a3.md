**P8.3** Repeat Exercise P8.2, but allow the user to specify the file name on the command-line. If the user doesn’t specify any file name, then prompt the user for the name.

**P8.4** Write a program that reads a file containing two columns of floating-point numbers. Prompt the user for the file name. Print the average of each column.

**P8.5** Write a program that searches all files specified on the command line and prints out all lines containing a keyword. For example, if you call

```
find Tim report.txt address.txt homework.cpp
```

then the program might print

```
report.txt: discussed the results of my meeting with Tim T
address.txt: Torrey, Tim|11801 Trenton Court|Dallas|TX
address.txt: Walters, Winnie|59 Timothy Circle|Detroit|MI
homework.cpp: Time now;
```

The keyword is always the first command-line argument.

**P8.6** Write a program that checks the spelling of all words in a file. It should read each word of a file and check whether it is contained in a word list. A word list is available on most UNIX systems (including Linux and Mac OS X) in the file `/usr/share/dict/words`. (If you don’t have access to a UNIX system, you can find a copy of the file on the Internet by searching for `/usr/share/dict/words`.) The program should print out all words that it cannot find in the word list. Follow this pseudocode:

+   Open the dictionary file.
+   Define a vector of strings called words.
+   For each word in the dictionary file
+    Append the word to the words vector.
+   Open the file to be checked.
+   For each word in that file
+    If the word is not contained in the words vector
+     Print the word.

**P8.7** Write a program that reads each line in a file, reverses its characters, and writes the resulting line to another file. Suppose the user specifies `input.txt` and `output.txt` when prompted for the file names, and `input.txt` contains the lines

```
Mary had a little lamb
Its fleece was white as snow
And everywhere that Mary went
the lamb was sure to go.
```

After the program is finished, `output.txt` should contain

```
bmal elttil a dah yraM
wons sa etihw saw eecelf stI
tnew yraM tahw erehwreve dnA
.og ot erus saw bmal eht
```

**P8.8** Write a program that reads each line in a file, reverses its characters, and writes the resulting line to the same file. Use the following pseudocode:

+   While the end of the file has not been reached
+    pos1 = current get position
+    Read a line.