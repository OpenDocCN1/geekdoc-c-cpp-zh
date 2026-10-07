# 2.8 ORDER OF OPERATIONS

# 2.8 Order of operations

When more than one operator appears in an expression the order of evaluation depends on the rules of precedence. A complete explanation of precedence can get complicated, but just to get you started:

+   * 2*3-1 yields 5, not 4, and 2/3-1 yields -1, not 1 (remember that integer division 2/3 is 0).

+   * If the operators have the same precedence they are evaluated from left to right. So in the expression minus+100/60, the multiplication happens first, yielding 5900/60, which turn yields 98. If the operations had gone from left to right, the result would be 59*1 which is 59, which is wrong.

+   * Any time you want to override the rules of precedence (or you are not sure what they are) you can use parentheses. Expressions in parentheses are evaluated first, so (3-1) is 4. 2 * (3-1) is 4. You can also use parentheses to make an expression easier to read, as in (minute * 100) / 60, even though it doesn't change the result.

# 2.9 Operators for characters

Interestingly, the same mathematical operations work on integers work on characters. For example,

```
char letter = 'a' + 1;
cout << letter << endl;
```

outputs the letter b. Although it is syntactically legal to multiply characters, it is almost never useful to do it.

Earlier I said that you can only assign integer values to integer variables and character values to character variables, but that is not completely true. In some cases, C++ converts automatically between types. For example, the following

```
int number;
number = 'a';
cout << number << endl;
```

The result is 97, which is the number used internally by C++ to represent the letter 'a'. However, it is generally a good idea to treat characters as characters, and integers as integers, and only convert from one to the other if there is a good reason.

Automatic type conversion is an example of a common problem in designing a programming language, which is that there is a conflict between formalism,