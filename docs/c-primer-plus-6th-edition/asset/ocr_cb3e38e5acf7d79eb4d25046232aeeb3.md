# Chapter 6 Branching Statements and Logical Operators

Here's a sample run of the program in Listing 6.12:

```
Enter a line of text:
Let's do lunch today. You can pay!
Complete line:
Let's do lunch today. You can pay!
Line through first period:
Let's do lunch today.
3 spaces
Done.
```

# Program Notes

Note that whereas the continue statement causes the program in Listing 6.12 to skip the rest of the loop, it doesn't skip the loop update expression. In a for loop, the continue statement makes the program skip directly to the update expression and then to the test expression. For a while loop, however, continue makes the program directly to the test expression. So any update expression in a while loop following the continue would be skipped. In some cases, that could be a problem.

This program doesn't have to use continue. Instead, it could use this code:

However, the continue statement can make a program more readable when several statements follow the continue. That, you don't need to make all those statements part of an if statement.

C++, like C, also has a goto statement. A statement like this means to jump to the location bearing the paris: label:

```
goto paris;
```

That, you can have code like this:

```
char ch;
cin >> ch;
if (ch == 'p')
goto paris;
cout << <<
...
```

```
paris: cout << "You've just arrived at Paris.\\n";
```

In some circumstances (some would say in all circumstances), goto is a bad hack, and you should use structured controls, such as if else, switch, continue, and the like, to control program flow.