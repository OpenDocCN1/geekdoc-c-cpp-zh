```
$ cat students
John Johnsen      john.johnsen@tp.com      503.555.1111
Hassaan Sarwar    hsarwar@k12.st.or        503.444.2132
David Kendall     d_kendall@msnbc.org      229.111.2013
John Johnsen      j.johnsen@psu.net        301.999.8888
Ibraheem Sarwar   ibraheem@abc.sci.com     222.123.4567
Kelly Kimberly    kellyk@umich.gov         555.123.9999
Maham Sarwar      smsarwar@k12.st.or       713.888.0000
Jamie Davidson    j.davidson@uet.edu       515.001.1212
Sandy Khan        sandy.khan@isu.edu       515.101.9009
Nabeel Sarwar     n.sarwar@xyz.net         434.555.1212
$
```

The most common and simple use of the grep utility is to display the lines in a file containing a particular string, word, or pattern. In the following session, we display those lines in the students file that contain the string Sarwar. The lines are displayed in the order they occur in the file.

```
$ grep Sarwar students
Hassaan Sarwar    hsarwar@k12.st.or        503.444.2132
Ibraheem Sarwar   ibraheem@abc.sci.com     222.123.4567
Maham Sarwar      smsarwar@k12.st.or       713.888.0000
Nabeel Sarwar     n.sarwar@xyz.net         434.555.1212
$
```

The grep command can be used with the -n option to display the output lines with line numbers. In the following session, the lines in the students file containing the string John are displayed with line numbers.

```
$ grep -n John students
1: John Johnsen    john.johnsen@tp.com      503.555.1111
4: John Johnsen    j.johnsen@psu.net        301.999.8888
$
```

You can use the grep command to search a string in multiple files with regular expressions and shell metacharacters. In the following session, grep searches for the string “include” in all the files in the present working directory that end with .c (C source files). Note that the access permissions for server.c were set so that grep couldn’t read it; the user running the command did not have the read permission for the server.c file.

```
$ grep -n include *.c
client.c: 21: #include <stdio.h>
client.c: 22: #include <ctype.h>
client.c: 23: #include <string.h>
labl.c:  13: #include <stdio.h>
grep: can’t open server.c
$
```

You can also use the grep command with the -l option to display the names of files in which the pattern occurs. However, it does not display the lines that contain the pattern. In the following session, the ~/States directory is assumed to contain one file for every US state, and this file is assumed to contain the names of all the cities in the state (e.g., Portland). The grep command, therefore, displays the names of files that contain the word “Portland”—that is, the names of states that have a city called Portland.

```
$ grep -l Portland ~/States
Maine
Oregon
$
```