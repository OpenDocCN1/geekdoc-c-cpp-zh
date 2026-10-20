
```
$ which cat
/bin/cat
$ which ftp
/usr/bin/ftp
$ which tar
/bin/tar
$
```

When a command does not work according to its specification, the which utility can be used to determine the absolute pathname of the command version that executes. A local version of the command may execute because of the way the search path is set up in the PATH variable (see Chapters 2 and 4). And, the local version has been broken due to a recent update in the code; perhaps it does not work properly with the new libraries that were installed on the system. The which command takes **command-list** (actually a **file-list** for the commands) as an argument and returns absolute pathnames for them to standard output.

In the following in-chapter exercises, you will get practice using the find, sort, and whereis commands, as well as appreciate the difference between the find and whereis commands.

+   **Exercise 7.4**  
+   Give a command for sorting a file called **students** by using the whole line starting with the e-mail address.
+   
+   **Exercise 7.5**  
+   Give a command for finding out where the executable code for the `traceroute` command is on your system.
+   
+   **Exercise 7.6**  
+   You have a file called **phones** somewhere in your directory structure, but you do not remember the pathname of the directory it is in. What command would you use to locate it?

## 7.4 Regular Expressions

A *regular expression* is a sequence of constants and operator symbols (known as operators) that represents a set of strings, commonly known as *search patterns*. Most of the Linux utilities operate on text files a line at a time. Regular expressions are used for searching file contents for the desired patterns on a single line. They may not be used to search for patterns that start on one line and end on another.

Regular expressions allow you to search for strings of a certain size. You can search for strings with particular patterns of letters, numbers, and punctuation marks. You can search for a word that starts and ends with a vowel, and has two consecutive “l” letters. What you do with the strings identified by a regular expression that depends on the tool that you use to identify them. Text editor such as vim can replace them with new strings. Some simply display them on the screen.

Some of the shell metacharacters are similar to the operators used in regular expressions. Although metacharacters in a command line are processed and expanded by the shell before passing them to the command, regular expressions are handled by the command. Bourne shell, Bash, C shell, and utilities such as find and cpio use metacharacters and not regular expressions. On the other hand, utilities such as awk, egrep, emacs, expr, grep, more, perl, python, sed, and vim use regular expressions. To prevent the shell from processing them, operators in a regular expression must be quoted when passed as an option in a shell command.

Different utilities in Linux support different sets of operators, but the following operators are supported by almost all Linux tools that support regular expressions: (), [], ., ^, $, and *. Some use additional operators like |, ?, and +. Table 7.1 shows the purpose of these and other operators with examples.

The * operator may be used to specify zero or more occurrences of the preceding element. For example, a* represents an empty string, a, aa, aaa, and so on. The expression .com matches strings Acom, acom, Bcom, bcom, Ccom, ccom, and so on. Similarly, the expression A.B matches AAB, ABB, ACB, A0B, A1B, A2B, etc. It is important to note that regular expressions match the longest possible pattern. That is, the regular expression A.*B matches “AAB” as well as “AAAABBABBBCCCCAAABCDEFBBBAAAB.” It is not the

**TABLE 7.2**

*Examples of Regular Expressions for vim and Their Meaning*

| Regular Expression | Meaning | Examples |
|---|---|---|
| `/^Yes/` | A line starting with the string **Yes** | **Yes**…<br>**Yes**teryear…<br>**Yes**terday…<br>and so on |
| `/th/` | Occurrence of the string **th** anywhere in a word | **the**, there, pa**th**, ba**th**ing, and so on |
| `/:$/` | A line ending with a colon | … following:<br>… below:<br>… follows:<br>and so on |
| `/[0-9]/` | A single digit | 0, 1, …, 9 |
| `[a-z][0-9]/` | A single lowercase English letter followed by a single digit | a0, a1, …, a9, …, b0, b1, …, b9, …, z0, … z1, …, z9 |
| `/\.c/` | Any word that ends with **.c** (all C source code files) | **lab1.c**, **program1.c**, **client.c**, **server.c**, and so on |
| `/[a-zA-Z ]*/` | Any string composed of letters (uppercase or lowercase) and spaces; no numbers and punctuation marks | All strings without numbers and punctuation marks such as **Hello world** |

**TABLE 7.3**

*Some Commonly Used vim Commands Illustrating the Use of Regular Expressions*

| Command | Meaning |
|---|---|
| `/ [0-9] /` | Do a forward search for a single stand-alone digit character in the current file; digits that are part of strings are not identified. |
| `?\.c[1-7] ?` | Do a backward search for words or strings in words that end with `.c` followed by a single digit between 1 and 7. |
| `:1,$s/:$/./` | Search the whole file and substitute a colon (`:`) at the end of a line with a period (`.`). |
| `:.,$s/^\[Hh]ello /Greetings /` | From the current line to the end of file, substitute the words “Hello” and “hello” starting a line with the word “Greetings.” |
| `:1,$s/^ *//` | Eliminate one or more spaces at the beginning of all the lines in the file. |

using “\” followed by a single digit starting with 1. Thus, the regular expression “\([0-9]\)\1” matches two identical digits such as 33 and 99.

Some of the commonly used Linux tools that allow the use of regular expressions are awk, ed, egrep, grep, sed, vi, and vim, but the level of support for regular expressions isn’t the same for all these tools. Although awk and egrep have the best support for regular expressions, grep has the weakest.

Table 7.1 lists the regular expression operators, their names, example usage, meanings, and tools that support them. The regular expression operators overlap with shell metacharacters, but you can use single quotes around them to prevent the shell from interpreting them. The word “All” in the last column means that all Linux utilities support the corresponding operator. We do not use quotes for strings in the fourth column for brevity.

Table 7.2 lists some commonly used regular expressions in the vim editor and their meanings. Needless to say, regular expressions are used in the vim commands. We discuss examples for grep and egrep in Section 7.6. In the regular expression /^\.c/, the backslash character (\) is used to escape the special meaning of dot (.) and take its literal meaning.

Table 7.3 lists some examples of the vim commands that use regular expressions and their meaning. Note that these commands are used when you are in vim’s command mode.

In the following in-chapter exercises, you will use regular expressions in the vim editor to appreciate their power.

## Exercise 7.7

List the strings that regular expression “\([0-9]\)\1\1” matches?

## Exercise 7.8

Create a file that contains the words “Linux,” “UNIX,” “Windows,” and “DOS.” Be sure that some of the lines in this file end with those words. Replace the string Windows with Linux in the whole document as you edit it with the vim editor. What command(s) did you use?

## Exercise 7.9

As you edit the document in Exercise 7.8, in a vim, run the command :1,$s/DOS\./LINUX\./gp. What did the command do to the document?

## Exercise 7.10

Create a file called testregex that has several (but not all) lines containing words express, expressing, expression, expressions, and expresses. What do you think would be the effect of executing the :1,$s/e....ss/DOODLING/gp command while editing testregex. Now edit the file with vim and run the command. What did the command do to the document? Does the result make sense? Why or why not?

## 7.5 Searching Files

Linux has powerful utilities for file searching that allow you to find lines in text files that contain a particular expression, string, or pattern. For example, if you have a large file that contains the records for a company’s employees, one per line, you might want to search the file for line(s) containing information on John Johnsen. The utilities that allow file searching are grep, egrep, and fgrep. The following is a brief description of these utilities.

```
Syntax:
 grep [options] pattern [file-list]
 egrep [options] [string] [file-list]
 fgrep [options] [expression] [file-list]
```

Purpose: Search the files in file-list for the given pattern, string, or expression; if no file-list, take input from standard input

Output: Lines containing the given pattern, string, or expression on standard output

# Commonly used options/features:

+   -c Print the number of matching lines only
+   -i Ignore the case of letters during the matching process
+   -l Print only the names of files with matching lines
+   -n Print line numbers along with matched lines
+   -r Read files under a directory (home directory if none is specified) recursively; following symbolic links only if they are specified on command line
+   -s Useful for shell scripts; suppresses error messages (the return status is set to zero for success and nonzero for no success—see Chapter 10)
+   -v Print nonmatching lines
+   -w Search for the given pattern as a string

Of the three, the fgrep command is the fastest but most limited; egrep is the slowest but most flexible, allowing full use of regular expressions; and grep has reasonable speed and is fairly flexible in terms of its support of regular expressions. In the following sessions, we illustrate the use of these commands with some of the options shown in the description. We use the same students file in these sessions that we use in describing the sort utility in Section 7.3. We display the file by using the cat command.
