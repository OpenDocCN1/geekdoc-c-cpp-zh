characters '1' and '0', not the number 10. This conversion between characters and numbers is usually done automatically so that you need not think about such details; however, sometimes all this automatic help gets in the way. Therefore, C++ provides some low-level facilities for input and output of character data. These low-level facilities include no automatic conversions. This allows you to bypass the automatic facilities and do input/output in absolutely any way you want. You could even write input and output functions that can read and write int values in Roman numeral notation, if you wanted to be so perverse.

# The Member Functions get and put

The function get allows your program to read in one character of input and store it in a variable of type char. Every input stream, whether it is an input-file stream or the stream cin, has get as a member function. We will describe get here as a member function of the object cin. (When we discuss file I/O in Chapter 12 we will see that it behaves exactly the same for input-file streams as it does for cin.)

Before now, we have used cin with the extraction operator, >>, in order to read a character of input (or any other input, for that matter). When you use the extraction operator >>, some things are done for you automatically, such as skipping over whitespace. But sometimes you do not want to skip over whitespace. The member function cin.get reads the next input character no matter whether the character is whitespace or not.

cin.get

The member function get takes one argument, which should be a variable of type char. That argument receives the input character that is read from the input stream. For example, the following will read in the next input character from the keyboard and store it in the variable nextSymbol:

```
char nextSymbol;
 cin.get(nextSymbol);
```

reading blanks and '\n'

It is important to note that your program can read any character in this way. If the next input character is a blank, this code will read the blank character. If the next character is the newline character '\n' (that is, if the program has just reached the end of an input line), then the previous call to cin.get will set the value of nextSymbol equal to '\n'. For example, suppose your program contains the following code:

```
char c1, c2, c3;
 cin.get(c1);
 cin.get(c2);
 cin.get(c3);
```

and suppose you type in the following two lines of input to be read by this code:

AB
CD

The value of c1 is set to 'A', the value of c2 is set to 'B', and the value of c3 is set to '\n'. The variable c3 is not set equal to 'C'.