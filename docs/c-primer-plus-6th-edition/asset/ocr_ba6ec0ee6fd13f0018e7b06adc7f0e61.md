# Introducing for Loops

The loop update part of the loop uses the ++ operator, called the increment operator. It increments the value of its operand by 1. (The increment operator is not restricted to loops. For example, you can use i++; instead of i = i + 1; as a statement in a program.) Incrementing i completes the first cycle of the loop.

Next, the loop begins a new cycle by comparing the new i value with 5. Because the new value (1) is also less than 5, the loop prints another line and finishes by incrementing again. That sets the stage for a fresh cycle of testing, executing a statement, updating the value of i. The process continues until the loop updates to 5. Then the next test fails, and the program moves on to the next statement after the loop.

# Parts of for Loop

A for loop provides a step-by-step recipe for performing repeated actions. Let's take a more detailed look at how it sets up. The usual parts of a for loop handle these steps:

+   1. Setting a value initially
2. Performing a test to see whether the loop should continue
3. Executing the loop actions
4. Updating value(s) used for the test

The C++ loop design positions these elements so that you can spot them at a glance. The initialization, test, and update actions constitute a three-part control section enclosed in parentheses. Each part is an expression, and semicolons separate the expressions from each other. The statement following the control is called the body of the loop, and it is executed as long as the expression remains true:

```
for (initialization; test-expression; update-expression)
    body
```

C++ syntax counts a for statement as a single statement, even though it can incorporate one or more statements in the body. (Having more than one statement requires a compound statement, or, as discussed later in this chapter.)

The loop performs initialization just once. Typically, programs use this expression to set a variable to a starting value and then the variable to count loop cycles. test-expression determines whether the loop body executes. Typically, this expression is a relational expression—that is, compares two values. Our example compares the value of i to 5, checking whether i is less than 5. If the comparison is true, the program executes the loop body. C++ doesn't limit test-expression to true/false expressions. You can use any expression, and C++ will cast it to type bool. Then expression with 0 is converted to the bool value false, and the loop terminates. If the expression evaluates to nonzero, it is cast to the bool value true, and the loop continues. Listing 5.2 demonstrates this by using the expression i as the test condition. (In the update section, i-- is similar to i++ except that it decreases the value of i by 1 each time it's used.)