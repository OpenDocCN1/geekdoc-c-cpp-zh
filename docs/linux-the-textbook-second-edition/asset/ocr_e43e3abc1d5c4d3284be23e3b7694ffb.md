```
Hamid
Ira
Jamal
$ head -5 sample
Ann
Ben
Chen
David
Eto
$
```

You can display heads of multiple files by specifying them as arguments of the head command. For example, the head sample memo1 phones command displays the first ten lines each of the sample, memo1, and phones files. The head of each file is preceded by ==> filename <= at the top left.

The following command, which displays the first ten lines of the file otto, shows that the file is a PostScript file. The output of the command gives additional information about the file, including the name of the software used to create it, the total number of pages in the file, and the page orientation. All of this information is important to know before the file is printed.

```
$ head otto
%!PS-Adobe-3.0
%%BoundingBox: 54 72 558 720
%%Creator: Mozilla (Firefox) HTML->PS
%%DocumentData: Clean7Bit
%%Orientation: Portrait
%%Pages: 1
%%PageOrder: Ascend
%%Title: Otto Doggie
%%EndComments
%%BeginProlog
$
```

Similarly, the following command shows that data is a uuencoded file and that, when uudecoded (see Chapter 7), the original file will be stored in the file data.99.

```
$ head -4 data
begin 600 data.99 M.0I$3T4L($I0 92!# .B`@,#`P.3`P.3H@0T4Z(` `@(`@(`!34CH@9&]E,4!S M;6EL92YC;VTZ(#4P,RXR,C(N,C(R,CH0~3`S+C,S,RXS,S,S"E-A<G=A<BP@ M4WEE9"!-.C`P,#$P- 34Z144Z4U(Z< V%R=R%R0`5P+FSD=3HU,#,N,3SQ+CSR
$
```

The tail command is used to display the last portion (tail) of one or more files. It is useful to ascertain, for example, that a PostScript file has a proper ending or that a uuencoded file has the required end on the last line. The following is a brief description of the command.

Syntax:
    tail [option] [file-list]
Purpose: Display the last portions (i.e., tails) of files in file-list; the default tail size is ten lines
Output: Tails of the files in file-list displayed on the monitor screen
Commonly used options/features:
    -f    Follow growth of the file after displaying its tail and display lines, as they are appended to the file. The tail command run with this option is terminated with <Ctrl+C>
    ±n    Start n lines from the beginning of the file for +n, and n line (or n units) before the end of the file for -n; by default, n is 10
    -n N  Display first N lines
    -r    Display lines in the reverse order (last line first)