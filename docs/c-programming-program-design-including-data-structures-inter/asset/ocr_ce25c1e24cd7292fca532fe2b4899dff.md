# ### Choosing the Right Looping Structure

All three loops have their place in C++. If you know, or the program can determine in advance, the number of repetitions needed, the for loop is the correct choice. If you do not know, and the program cannot determine in advance the number of repetitions needed, and it could be 0, the while loop is the right choice. If you do not know, and the program cannot determine in advance the number of repetitions needed, and it is at least 1, the do...while loop is the right choice.

# ## break and continue Statements

The break statement, when executed in a switch structure, provides an immediate exit from the switch structure. Similarly, you can use the break statement in while, for, and do...while loops. When the break statement executes in a repetition structure, it immediately exits from the structure. The break statement is typically used for two purposes:

+   - To exit early from a loop.
+   - To skip the remainder of the switch structure.

After the break statement executes, the program continues to execute with the first statement after the structure. The use of a break statement in a loop can eliminate the use of certain flag variables. The following C++ code segment helps illustrate this idea. (Assume that all variables are properly declared.)

```
    sum = 0;
    isNegative = false;

    cin >> num;

    while (cin && !isNegative)
    {
        if (num < 0)    //if num is negative, terminate the loop
                        //after this iteration
        {
            cout << "Negative number found in the data." << endl;
            isNegative = true;
        }
        else
        {
            sum = sum + num;
            cin >> num;
        }
    }
```

This while loop is supposed to find the sum of a set of positive numbers. If the data set contains a negative number, the loop terminates with an appropriate error message. This while loop uses the flag variable isNegative to accomplish the desired result. The variable isNegative is initialized to false before the while loop. Before adding num