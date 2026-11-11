# # Chapter 7: The Conditional Statements

C# has conditional statements, mostly used for controlling the flow of execution. The conditional statements expect the programmer to specify a condition or a set of conditions and the corresponding set of statements to be executed if a condition is found to be true. The programmer can also specify the set of statements that are to be executed if the condition is not true.

Let us discuss the various conditional statements supported in C#.

# ## if Statement

This statement is used to evaluate a Boolean expression before a set of statements can be executed. If the condition stands true, then there will be execution of one set of statements, otherwise, another set of statements will be executed. Here is the syntax for this statement:

```
    if(boolean_expression) {
        /* statement(s) to execute if above boolean expression is true */
    }
```

Here is an example:

```
    using System;
    namespace DecisionMaking {
        class IfStatement {
            static void Main(string[] args) {
                /* defining a local variable */
                int x = 5;
                /* check a boolean condition via if statement */
                if (x < 10) {
                    /* to be printed of the condition is true */
                    Console.WriteLine("x is less than 10");
                }
                Console.WriteLine("The value of x is : {0}", x);
                Console.ReadLine();
            }
        }
    }
```

The code returns the following output: