This design still follows the precept of attempting to read before testing because we evaluate the expression inFile >> value, the program first has to attempt to read a number into value.

Now you know the rudiments of file I/O.

# Summary

Programs and programming become more interesting when you introduce statements that guide the program through alternative actions. (Whether this also makes the programmer more interesting is a point you may wish to investigate.) C++ provides the if statement, the else statement, and the switch statement as for managing block choices. The C++ if statement lets a program execute a statement or block if a particular condition is met. The C++ if else statement lets a select from two choices which statement or block to execute. You can append additional if else statements to a statement for a series of choices. The C++ switch statement directs the program to a list of choices.

C++ also provides operators to help in decision making. Chapter 5 discusses the relational expressions, which compare two values. The if and else statements typically use relational expressions as test conditions. By using C++ logical operators (&, ||, !),you can combine or modify relational expressions to construct more elaborate tests. The conditional operator (?:) provides a compact way to choose from two values.

The ctype library of character functions provides a convenient and powerful set of tools for analyzing character input.

Loops and selection statements are useful tools for file I/O, which closely parallels console I/O. After you declare ifstream and ostream and associate them with files, you can use these objects in the same manner using cin and cout.

C++'s loops and decision-making statements, have the tools for writing interesting, intelligent, and powerful programs. But we've only begun to investigate the real powers of C++. Next, we'll look at functions.

# Chapter Review

+   1. Consider the following code fragments for counting spaces and newlines:

```
// Version 1
while (cin.get(ch)) // quit on eof
{
    if (ch == ' ')
        spaces++;
    if (ch == '\n')
        newlines++;
}
```

```
// Version 2
```