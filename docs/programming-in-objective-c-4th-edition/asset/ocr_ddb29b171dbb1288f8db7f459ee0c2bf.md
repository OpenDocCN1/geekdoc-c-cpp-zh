This statement assigns the value of TRUE to gameOver. You don’t need to concern yourself with the actual value you defined for TRUE, but because you know that you defined it to be 1, the preceding statement would have the effect of assigning 1 to gameOver. The preprocessor statement

```
#define FALSE 0
```

defines the name FALSE makes its subsequent use in the program equivalent to specifying the value 0. Therefore, the statement

```
gameOver = FALSE;
```

assigns the value of FALSE to gameOver, and the statement

```
if ( gameOver == FALSE )
...
```

compares the value of gameOver against the defined value of FALSE.

A defined name is not a variable. Therefore, you cannot assign a value to it unless the result of substituting the defined value is a variable. Whenever a defined name is used in the program, the preprocessor automatically substitutes into the program whatever appears to be the right of the defined name in the #define statement. It’s analogous to a search and replace with a text editor; in this case, the preprocessor replaces all occurrences of the defined name with its associated text.

Note that the #define statement has a special syntax: No equals sign is used to assign the value 1 to TRUE. Furthermore, a semicolon does not appear at the end of the statement. Soon you will understand why this special syntax exists.