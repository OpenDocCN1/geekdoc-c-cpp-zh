# 18 Learning SAS by Example: A Programmer’s Guide, Second Edition

Because exponentiation and negation occur first, you have the following equation:

```
x = 8 + 4 * -5;
```

This gives you:

```
8 + (-20) = -12
```

# 2.3 More on Comment Statements

Another way to add a comment to a SAS program is to start it with a slash (/) and end it with a slash (*/). You may even embed comments of this type within a SAS statement. For example, you could write:

```
input Gender $ Age /* * age is in years */ Height Weight;
```

If you are using a mainframe computer, you may want to avoid starting your /* in column one because the operating system will interpret it as control language (JCL) and terminate your SAS job.

Be sure that you do not nest the /* style comments. For example, you would get an error if you submitted Program 2.3. The first /* (also shown in bold) would match the first /* (also shown in bold), leaving invalid SAS code to be processed.

# Program 2.3: Incorrect Nesting of /* /* Style Comments

> * This comment contains a /* style * comment embedded within another comment. Notice that the first star ends the comment and the remaining portion of the comment will cause a syntax error /*

# 2.4 How SAS Works (a look inside the “Black Box")

This is a good time to explain some of the inner workings of SAS as it processes a DATA step. Looking again Program 2.2, let’s “play computer.” SAS processes DATA steps in two stages—compile step and execution step.

Here’s how SAS recognizes the DATA step and understands. In the compile step, it does some housekeeping tasks. First, it prepares an area to store the SAS data set (Demographic). It checks the input file (described by the INFILE name) and various attributes of this file (such as the length of each record). Next, it sets aside a place in memory called the input buffer, where it will place each record (line) of data as it is read from the input file. It reads each line of the program, for invalid syntax, and determines the name of all the variables that are in the data set. Depending on your INPUT statement (or other statements), SAS determines whether each variable is character or numeric and the storage length of each variable. This information is called the descriptor portion of the data set. In this compile step, data is read from the input file and no logical statements are evaluated. Each line is processed from order to the top and left to right.

In this example, SAS sees the first four variables in the INPUT statement, decides that Gender is character (because of the dollar sign ($) following the name), and sets the storage length of each of these variables. Because no lengths are specified by the program, each variable is given a default length (8 bytes