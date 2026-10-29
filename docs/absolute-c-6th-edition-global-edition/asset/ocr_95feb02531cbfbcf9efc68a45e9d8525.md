With the function cin.getline, the entire line is read. The reading ends when the line ends, even though the resulting C-string may be shorter than the maximum number of characters specified by the second argument.

When getline is executed, the reading stops after the number of characters given by the second argument has been filled in the C-string array, even if the end of the line has not been reached. For example, consider the following code:

```
char shortString[5];
cout << "Enter some input:\n";
cin.getline(shortString, 5);
cout << shortString << " END OF OUTPUT\n";
```

When embedded in a complete program, this code produces a dialogue like the following:

```
Enter some input:
dobedowap
dobeEND OF OUTPUT
```

Notice that four, not five, characters are read into the C-string variable shortString, even though the second argument is 5. This is because the null character '\0' fills one array position. Every C-string is terminated with the null character when it is stored in a C-string variable, and this always consumes one array position.

The C-string input and output techniques we illustrated for cout and cin work the same way for input and output with files. The input stream cin can be replaced by an input stream that is connected to a file. The output stream cout can be replaced by an output stream that is connected to a file. (File I/O is discussed in Chapter 12.)

# getline

The member function getline can be used to read a line of input and place the string of characters on that line into a C-string variable.

# SYNTAX

```
cin.getline (String_Var, Max_Characters + 1);
```

One line of input is read from the stream Input_Stream and the resulting C-string is placed in String_Var. If the line is more than Max_Characters long, only the first Max_Characters on the line are read. (The +1 is needed because every C-string has the null character '\0' added to the end of the C-string and thus the string stored in String_Var is one longer than the number of characters read in.)

# EXAMPLE

```
char oneLine[80];
cin.getline(oneLine, 80);
```

As you will see in Chapter 12, you can use an input stream connected to a text file in place of cin.