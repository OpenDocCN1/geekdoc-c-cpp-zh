```
```cpp
int calculate(int param) {
    vector<int> data(/*...*/);
    // ...
    return result;
}
```
```

At the end of `calculate()`, *data* is automatically removed, no matter what you did with it in the function. The functionality is quite simple: The computer literally manages a *stack*, on which it always places the variables you define. The compiler keeps track of the positions in the stack where a range was entered—for example, with an opening block brace `{`. Upon leaving the range with the closing block brace `}`, the stack is unwound to the last marked position—see Figure 20.4.

![](bbox=[0.14, 0.37, 0.86, 0.72])

**Figure 20.4** Automatic variables are managed on the stack.

This stack thus manages the *automatic variables*. Whenever a variable leaves its scope, the system removes it along with its associated resources.