+   Recursive case: If n >= 10, then do two subtasks:
+   1. Output all the digits except the last digit.
+   2. Output the last digit.

For example, if the argument were 1234, the first subtask would output
1
2
3

and the second subtask would output 4. This decomposition into subtasks can be used to derive the function definition.

Subtask 1 is a smaller version of the original task, so we can implement this subtask with a recursive call. Subtask 2 is just the simple case we listed above. Thus, an outline of our algorithm for the function writeVertical with parameter n is given by the following pseudocode:

```
if (n < 10)
{
    cout << n << endl;
}
else //n is two or more digits long:
{
    writeVertical(the number n with the last digit removed);
    cout << the last digit of n << endl;
}
```

If you observe the following identities, it is easy to convert this pseudocode to a complete C++ function definition:
n/10 is the number n with the last digit removed.
n%10 is the last digit of n.

For example, 1234/10 evaluates to 123, and 1234%10 evaluates to 4.

The complete code for the function is as follows:

```
void writeVertical(int n)
{
    if (n < 10)
    {
        cout << n << endl;
    }
    else //n is two or more digits long:
    {
        writeVertical(n/10);
        cout << (n%10) << endl;
    }
}
```