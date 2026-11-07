applicable, the switch statement provides an easy-to-read, easy-to-modify alternative.

# The do-while Loop

For many repetition problems in C++, the condition to be tested comes at the beginning of the loop, before any statements are executed. This is normal for many situations, but there are situations where you might want to execute the body of the loop before the condition is tested. For these situations, C++ provides an alternative repetition statement, the do-while loop.

# Using the do-while Loop

The general form of the do-while loop is:

```
do
{
    set of statements;
} while (condition);
```

The condition that controls the loop is after the statements to be executed, which guarantees that the body of the loop will be executed at least once. This is not the case with a while loop, where if the condition isn't true before the first time into the loop, the loop doesn't execute at all.

The following example demonstrates the usefulness of the do-while loop. Here is a simple drill and practice program for addition that asks the user to solve a problem and then asks them if they would like to work another problem: