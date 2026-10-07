is no "above."

As a consequence, placing a semicolon after the Boolean expression following the if keyword will result in a compiler error. Since curly braces are not used, the if statement ends after the statement created by the incorrectly placed semicolon. The cout statement "The number is even" is not part of the if statement. Consequently, the else is not part of the if statement, and will be regarded as an else part without an if part.

```
if ( num % 2 == 0 ) { // don't put a semicolon here
cout << "The number is even" << endl;
else ( num % 2 == 1 ) {
cout << "The number is odd" << endl;
}
```

# Don't Put a Relational Expression after the else Keyword!

Another common mistake is to place a relational expression in parentheses after the else keyword. This will not cause a compiler or run-time error, but it will often cause an illogical result.

```
if ( num % 2 == 0)
cout << "The number is even" << endl;
else ( num % 2 == 1 )
cout << "The number is odd" << endl;
```

Actually, the error description is misleading. There is nothing wrong with the cout statement. No relational expression should follow the else keyword. The reason is that the else acts like "none of the above" in a multiple choice test. If the expression is not true, then the conditional statements connected to the else execute.

# Don't Put a Semicolon after the Else!

Another common mistake is to place a semicolon after the else expression. This too will not cause a compiler or run-time error, but often will cause an illogical result.

For example, in the following code, the cout statement "The number is odd" will output even if the number's input is even.

```
if ( num % 2 == 0 )
cout << "The number is even" << endl;
else; // don't put a semicolon here!
cout << "The number is odd" << endl;
```

The result of inputting an even number will be

Enter a whole number: 16nThe number is even
The number is odd

The cout statement "The number is odd" will execute whether or not the relational expression is true because the cout statement no longer is part of the if statement. Unless you use curly braces as explained already in connection with the if statement, the first statement following the else keyword is conditional. That, conditional is the empty statement by virtue of the semicolon following the expression. Therefore, the cout statement "The number is odd" is not part of the if statement at all.