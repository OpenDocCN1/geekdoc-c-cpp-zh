# DISPLAY 3.11 The for Statement (part 2 of 2)

```
3   {
4       cout << number
5       << " bottles of beer on the shelf.\n";
6       number--;
7   }
```

# Output

```
100 bottles of beer on the shelf.
99 bottles of beer on the shelf.
.
.
.
0 bottles of beer on the shelf.
```

Display 3.12 shows a sample for statement embedded in a complete (although very simple) program. The for statement in Display 3.12 is similar to the one discussed above, but it has one new feature. The variable n is declared when it is initialized to 1. So, the declaration of n is inside the for statement. The initializing action in a for statement can include a variable declaration. When a variable is used only within the for statement, this can be the best place to declare the variable. However, if the variable is also used outside of the for statement, then it is best to declare the variable outside of the for statement.

The ANSI C++ standard requires that a C++ compiler claiming compliance with the standard treat any declaration in a for loop initializer as if it were local to the body of the loop. Earlier C++ compilers did not do this. You should determine how your compiler treats variables declared in a for loop initializer. In the interests of portability, you should not write code that depends on this behavior. The ANSI C++ standard requires that variables declared in the initialization expression of a for loop be local to the block of the for loop. The next generation of C++ compilers will likely comply with this rule, but compilers presently available may or may not comply.

Our description of a for statement was a bit less general than what is allowed. The three expressions at the start of a for statement may be any C++ expressions and therefore they may involve more (or even fewer!) than one variable. However, our for statements will always use only a single variable in these expressions.

In the for statement in Display 3.12, the body was the simple assignment statement

```
sum = sum + n;
```

declaring variables within a for statement