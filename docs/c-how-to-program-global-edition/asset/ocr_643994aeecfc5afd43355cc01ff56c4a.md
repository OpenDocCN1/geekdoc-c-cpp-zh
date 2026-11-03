The comment in lines 1–2 states the purpose of the program. As we stated earlier, every program begins execution with `main`. The left brace `{` (line 7) marks the beginning of the body of `main`, and the corresponding right brace `}` (line 21) marks the end of `main`.

# Variables and Variable Definitions

Lines 8–9

```
    int integer1; // first number to be entered by user
    int integer2; // second number to be entered by user
```

are definitions. The names `integer1` and `integer2` are the names of variables—locations in memory where values can be stored for use by a program. These definitions specify that variables `integer1` and `integer2` are of type `int`, which means that they’ll hold integer values, i.e., whole numbers such as 7, –11, 0, 31914 and the like.

# Define Variables Before They Are Used

All variables must be defined with a name and a data type before they can be used in a program. The C standard allows you to place each variable definition anywhere in `main` before that variable’s first use in the code (though some older compilers do not allow this). You’ll see later why you should define variables close to their first use.

# Defining Multiple Variables of the Same Type in One Statement

The preceding definitions could be combined into a single definition as follows:

```
    int integer1, integer2;
```

but that would have made it difficult to associate comments with each of the variables, as we did in lines 8–9.

# Identifiers and Case Sensitivity

A variable name in C can be any valid identifier. An identifier is a series of characters consisting of letters, digits and underscores (`_`) that does not begin with a digit. C is case sensitive—uppercase and lowercase letters are different in C, so `a1` and `A1` are different identifiers.

> **Common Programming Error 2.2**
> 
> Using a capital letter where a lowercase letter should be used (for example, typing `Main` instead of `main`).

> **Error-Prevention Tip 2.1**
> 
> Avoid starting identifiers with the underscore character (`_`) to prevent conflicts with compiler-generated identifiers and standard library identifiers.

> **Good Programming Practice 2.5**
> 
> Choosing meaningful variable names helps make a program self-documenting—that is, fewer comments are needed.

> **Good Programming Practice 2.6**
> 
> The first letter of an identifier used as a simple variable name should be a lowercase letter. Later in the text we’ll assign special significance to identifiers that begin with a capital letter and to identifiers that use all capital letters.