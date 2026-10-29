When the body of the function is executed this time, something different happens. Since 1 is less than 10, the Boolean expression in the if-else statement is true, so the statement before the else is executed. That statement is simply a cout statement that writes the argument 1 to the screen, and so the call writeVertical(1) writes 1 to the screen and ends without any recursive call.

When the call writeVertical(1) ends, the suspended computation that is waiting for it to end resumes where that suspended computation left off, as shown by the following:

```
if (123 < 10)
{
}
else
{
}

if (12 < 10)
{
    cout << 12 << endl;
}
else //n is two or more digits long:
{
    writeVertical(12/10);
    cout << (12%10) << endl;
}
Computation resumes here.
```

When this suspended computation resumes, it executes a cout statement that outputs the value 12%10, which is 2. That ends that computation, but there is yet another suspended computation waiting to resume.

When this last suspended computation resumes, the situation is as follows:

```
if (123 < 10)
{
    cout << 123 << endl;
}
else //n is two or more digits long:
{
    writeVertical(123/10);
    cout << (123%10) << endl;
}
Computation resumes here.
```

This last suspended computation outputs the value 123%10, which is 3. The execution of the original function call then ends. And, sure enough, the digits 1, 2, and 3 have been written to the screen one per line, in that order.