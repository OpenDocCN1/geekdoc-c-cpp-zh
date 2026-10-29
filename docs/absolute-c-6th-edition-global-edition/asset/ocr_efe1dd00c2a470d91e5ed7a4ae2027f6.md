# Display 3.9 A Global Named Constant (part 2 of 2)

# Sample Dialogue

```
Enter a radius to use for both a circle
and a sphere (in inches) : 2
Radius = 2 inches
Area of circle = 12.5664 square inches
Volume of sphere = 33.5103 cubic inches
```

# Self-Test Exercises

20. If you use a variable in a function definition, where should you declare the variable? In the function definition? In the main function? Any place that is convenient?

21. Suppose a function named function1 has a variable named sam declared within the definition of function1, and a function named function2 also has a variable named sam declared within the definition of function2. Will the program compile (assuming everything else is correct)? If the program will compile, will it run (assuming that everything else is correct)? If it runs, will it generate an error message when run (assuming everything else is correct)? If it runs and does not produce an error message when run, will it give the correct output (assuming everything else is correct)?

22. What is the purpose of the comment that accompanies a function declaration?

23. What is the principle of procedural abstraction as applied to function definitions?

24. What does it mean when we say the programmer who uses a function should be able to treat the function like a black box? (This question is very closely related to the previous question.)

# Blocks

A variable declared inside a compound statement (that is, inside a pair of braces) is local to the compound statement. The name of the variable can be used for something else, such as the name of a different variable, outside the compound statement.

block

A compound statement with declarations is usually called a block. Actually, block and compound statement are two terms for the same thing. However, when we focus on variables declared within a compound statement, we normally use the term block rather than compound statement and we say that the variables declared within the block are local to the block.