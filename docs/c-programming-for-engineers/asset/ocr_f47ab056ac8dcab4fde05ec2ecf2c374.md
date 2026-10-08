Example: Swap the values of integers a and b.
Swapping or exchanging cannot work by doing this.

```
// this will not work
int a = 3, b = 5;
a = b;
a = a;
```

To swap the values of two integers, we need a temporary variable to store one of the values while we update the other. Here is an example:

```
int a = 3, b = 5, temp; // Declare a temporary variable 'temp'
```

```
// Swap the values of a and b using temp
temp = a;
a = b;
temp = temp;
```

```
printf("After swapping: a = %d, b = %d\n", a, b);
```

In the update code, the temporary variable temp is used to store the value of a before it is overwritten by the value of b. Then, a is assigned the value of b, and b is assigned the value stored in temp. This effectively swaps the values of a and b.

# 5.1.2 Compound Assignments

Compound assignment operators improve code readability by combining arithmetic operations with assignment in a single statement. This makes the modification of variables more efficient and easier to understand.

```
int total = 100;
total = total + 20; // Traditional
total += 20;       // Using compound assignment
```

Here, the += operator adds 20 to the current value of total and updates the variable in one step.

The compound assignment operator works on a limited set of operations as listed in Table 5.1.