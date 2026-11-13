To execute this recursive call, another activation record is created (with number now set to 3), and this activation record is pushed onto the run-time stack:

![](bbox=[0.31, 0.21, 0.8, 0.38])

The super_write_vertical function begins executing once more. With number set to 3, the function enters the section to handle a one-digit number. At this point, the digit 3 is printed, and no other work is done during this function call.

When the third function call ends, its activation record is popped off the stack. But just before it is popped, the activation record provides one last piece of information—telling where the computation should continue. In our example, the third activation record is popped off the stack, and the computation continues at Spot #2 in Figure 9.2 on page 440. At this point we have the two remaining activation records shown here:

![](bbox=[0.31, 0.55, 0.72, 0.7])

As we said, the computation is now at Spot #2 in Figure 9.2 on page 440. This is the highlighted location shown here:

```
else
{
    super_write_vertical(number/10);
    || This is Spot #2 referred to in the text.
    cout << number % 10 << endl;
}
```