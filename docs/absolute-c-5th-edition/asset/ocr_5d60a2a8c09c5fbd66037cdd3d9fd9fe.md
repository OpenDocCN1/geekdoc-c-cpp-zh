# CHAPTER 12 Streams and File I/O

+   11. Write a program that will correct a C++ program that has errors in which operator, << or >>, it uses with cin and cout. The program replaces each (incorrect) occurrence of

```
cin <<
```

with the corrected version

```
cin >>
```

and each (incorrect) occurrence of

```
cout >>
```

with the corrected version

```
cout <<
```

For an earlier version, assume that there is always exactly one blank symbol between any occurrence of cin and a following <<, and similarly assume that there is always exactly one blank space between each occurrence of cout and a following >>. For a harder version, allow for the possibility that there may be any of numbers, even zero blanks, between cin << and between cout >> in this harder case, the replacement corrected version has only one blank between the cin and the following operator. The program to be corrected is in one file and the corrected version is output to a second file. Your program should define a function that handles the input- streams (Hint: Even if you are doing the harder version, you will probably find it easier and quicker to first do the easier version and then modify your program so that it performs the harder task).

+   12. Write a program that allows the user to type in any one-line question and answers that answer the question, but will simply not really pay attention to the question line and discard all that it is. It always gives one of the following:

Im not sure but I think you will find the answer in Chapter #N.
That's a good question.
If I were you, I would not worry about such things.
That question has puzzled philosophers for centuries.
I don't know. I'm just a machine.
Think about it and the answer will come to you.
I used to know the answer to that question, but I've forgotten it.
The answer can be found in a secret place in the woods.

These answers are stored in a file (one answer per line), and your program simply reads the next answer from the file and writes it out as the answer to the question. After your program has read the entire file, it simply closes the file, reopens it, and starts down the list of answers again.