During several years of teaching C++ in an introductory programming class, I have noticed several common mistakes in the writing of statements. Some of these mistakes may result in compiler errors and are easy to stop. However, other mistakes are harder to pick out since they do not cause an error, either at compile time or run-time, but instead give rise to illogical results.

# Don't Put a Semicolon after the Relational Expression!

The first common mistake is to place a semicolon after the relational expression:

```
if ( num % 2 == 0 ); // don't put a semicolon here!
cout << "The number is even" << endl;
```

Since the compiler generally ignores blank spaces, the following if statement would be the same, and better illustrates visually:

```
if ( num % 2 == 0 )
    // don't put a semicolon here!
cout << "The number is even*" << endl;
```

No compiler error will result. The compiler will assume from the statement that it is an empty statement. An empty statement does nothing, and it is perfectly legal in C+, and indeed has some purpose, here it is intended.

One consequence will be that the empty statement will execute if the relational expression is true. If this comes, so far, there is no harm done.

However, there is an additional consequence, an illogical result. The code statement "The number is even" will execute whether or not the relational expression is true. In other words, if an odd number is entered, the program will output "The number is even."

Enter a whole number: 17
The number is even

The reason that the code statement will execute whether or not the relational expression is true is that the code statement is no longer part of the statement. Unless you use braces as explaining the first statement following the keyword and relational expression is conditional. That first conditional statement is the empty statement, by virtue of the semicolon following it if expression.

# Curly Braces Needed for Multiple Conditional Statements

As discussed

```
if ( num % 2 == 0 )
    cout << "The number is even" << endl;
cout << "And the number is not odd" << endl;
```

Note The indentation tells the programmer which statement is conditional and which is not. The compiler ignores indentation.

If the user enters an odd number like 17, the statement "The number is even" will not display because the relational expression is false. However, the following statement "And the number is not odd" will display that statement does not belong to the if statement.