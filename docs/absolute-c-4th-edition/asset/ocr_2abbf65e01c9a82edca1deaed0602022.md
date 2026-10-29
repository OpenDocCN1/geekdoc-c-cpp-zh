However, this can produce problems, as illustrated by the following dialogue:

```
Enter a number:
21
Now enter a letter:
A
```

With this dialogue, the value of number will be 21 as you expect. However, if you expect the value of the variable symbol to be 'A', you will be disappointed. The value given to symbol is '\n'. After reading the number 21, the next character in the input stream is the newline character. '\n', and so that is read next. Remember, get does not skip over line breaks and spaces. (In fact, depending on what is in the rest of the program, you may not even get a chance to type in the A. Once the variable symbol is filled with the character '\n', the program proceeds to whatever statement is next in the program. If the next statement sends output to the screen, the screen will be filled with output before you get a chance to type in the A.)

The following rewriting of the above code will cause the above dialogue to fill the variable number with 21 and fill the variable symbol with 'A':

```
cout << "Enter a number:\n";
int number;
cin >> number;
cout << "Now enter a letter:\n";
char symbol;
cin >> symbol;
```

Alternatively, you can use the function newLine, defined in Display 9.2, as follows:

```
cout << "Enter a number:\n";
int number;
cin >> number;
newLine();
cout << "Now enter a letter:\n";
char symbol;
cin.get(symbol);
```

As this second rewrite indicates, you can mix the two forms of cin and have your program work correctly, but it does require some extra care.

As a third alternative, you could use the function ignore, which we discuss in the next subsection.

# THE putback, peek, AND ignore MEMBER FUNCTIONS

Sometimes your program needs to know the next character in the input stream. However, after reading the next character, it might turn out that you do not want to process