Variables in C must be defined in a declaration statement that contains 1) the name of the variable and 2) the type of the variable. The value of the variable is optional. Variable declarations in C programs can appear before the main() code block, inside the main() function, or inside user-defined functions. Some developers think it’s better to define variables at the top of a function or near the block of code where they are used. Although opinions differ, the latter is common among object-oriented programming languages such as C++.

As a simple example, the following code snippet declares (but does not initialize) one variable of type integer, followed by a declaration of a second variable of type integer that is also initialized with an integer value:

```
int myInt1;
int myInt2 = 7;
```

Notice that variable declarations end with a semicolon. You can also define multiple variables of the same type in a single statement, as shown here:

```
int myInt1, myInt2 = 7, myInt3 = 25;
```

The general form of a variable declaration is:

```
type name; /* comment */
```

where type is one of the C variable types ( int, float, etc.) and name is any valid variable name in C.

# Assignment Statements

Assignment statements are used to give a value to a variable. The following code snippet is a very simple example of an assignment statement:

```
num = (1 + 2) * 4;
```