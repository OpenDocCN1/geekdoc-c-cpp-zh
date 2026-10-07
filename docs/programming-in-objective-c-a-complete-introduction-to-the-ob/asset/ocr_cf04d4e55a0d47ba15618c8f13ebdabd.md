# Chapter 12 The Preprocessor

literally substitutes 2.0 * 3.141592654 whenever the defined name TWO_PI occurs in the program.

The fact that the preprocessor performs a literal substitution whenever the defined name occurs explains why you would not want to end your #define statement with a semicolon. If you did, the semicolon would also be substituted into the program wherever the defined name appeared. If you defined PI as

```
#define PI 3.14159264;
```

and then written

```
return 2.0 * PI * r;
```

the preprocessor would replace the occurrence of the defined name PI by 3.141592654; The compiler would then end this statement as

```
return 2.0 * 3.141592654; * r;
```

after the preprocessor had made its substitution, which would result in a syntax error. Remember not to put a semicolon at the end of your define statements unless you're really sure you want one there.

A preprocessor definition does not have to be a valid Objective-C expression in its own right, as the resulting expression is valid wherever it is used. For instance, you could set up these definitions:

```
#define AND &&
#define OR ||
```

Then you could write expressions as such

```
if ( x > 0 AND x < 10 )
...
and
if ( y 0 OR y value )
..
```

You could include a #define for the equality test:

```
#define EQUALS =
```

Then, you could write the following statement:

```
if ( y EQUALS 0 OR y EQUALS value )
..
```

This removes the very real possibility of mistakenly using a single equals sign for the equality test.

Although these examples illustrate the power of the #define, you should note that it is commonly considered bad programming practice to redefine the syntax of the underlying language in such a manner. Plus, it makes harder for someone else to understand your code.