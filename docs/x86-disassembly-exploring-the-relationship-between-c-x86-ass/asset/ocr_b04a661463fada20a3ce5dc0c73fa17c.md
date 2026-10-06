```
inc ebx
cmp ebx, 100
jne _Label_1
mov esp,ebp
pop ebp
ret 4
```

Starting with the function prototype above, and the description of what this function does, we can start to write the code for this function. We know that this function initializes ebx, eax, and ecx before the loop. However, we can see that ecx is being used as a simple intermediate storage location, receiving successive values from the array, and then being added to ecx.

We will create two unsigned integer values, a (for eax) and b (for ebx). We will define both a and b with the register qualifier, so that we can instruct the compiler not to create space for them on the stack. For each loop iteration, we are adding the value of the array, at location eax to the running sum, eax. Converting this to our a and b variables, and using C syntax, we see:

```
a = a + array[b];
```

The loop could be either a for loop, or a while loop. We see that the loop control variable, b, is initialized to 0 before the loop, and is incremented by 1 each loop iteration. The loop tests b against 100, after it gets incremented, so we know that b never equals 100 inside the loop body. Using these simple facts, we will write the loop in 3 different ways:

First, with a while loop:

```
unsigned int STDCALL MyFunction(unsigned int *array)
{
    register unsigned int b = 0;
    register unsigned int a = 0;
    while(b != 100)
    {
        a = a + array[b];
        b++;
    }
    return a;
}
```

Or, with a for loop: