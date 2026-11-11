
For example, let the value of the variable x be initialized to 32, as shown below:

```c
int x = 32;
```

The statement,

```c
r = x >> 3;
```

will shift the bits in the number x by padding 3 extra 0s at the MSB side of x. The resultant number obtained after shifting the bits of x will be stored in the variable r, as shown below in Figure 3.16.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_104_0.png)

![](img/57c0d966bb33c67a5a188e6bf39e4e02_104_1.png)

Hence, the value of the variable r will be set as 4, which is the decimal equivalent of the binary number 100.

Note that the value of the variable x is 32 and after shifting 3 bit positions in x, we get the value of the variable r as 4, which can also be obtained from the original value 32, as shown below:

$$\frac{32}{2^3}=4$$

This means that when we apply a right shift operation on any number x by k bit positions, the result of the right shift operation is equivalent to the expression x/2ᵏ.

## 3.6 Increment/Decrement Operators

The increment operator is used to increase the value of the variable by 1 whereas the decrement operator can be used to decrease the value of the variable by 1. The symbol ++ (two consecutive plus signs without a space) represents an increment operation over a variable and the symbol, -- (two consecutive minus signs without a space) represents a decrement operation over a variable. The increment/decrement operators can be used in prefix or postfix form.

When an increment/decrement operator is used in the prefix form the value of the variable is incremented/decremented before it is used to evaluate the result of a particular

![](img/57c0d966bb33c67a5a188e6bf39e4e02_106_0.png)

**Figure 3.18.** Value of variables a and b

### 3.6.2 Increment operator in a postfix form

So as to understand the usage of increment operator in the postfix form, let us create two variables x and y as shown below:

```c
int x = 10, y;
```

As per the above statement, the value of variable x will be set as 10 and the value of the variable y will be junk at this stage as shown in Figure 3.19.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_106_1.png)

**Figure 3.19.** Value of variables x and y

Let us now apply a postfix increment operation on the variable x and initialize the result of the operation to the variable y. This can be done using the following statement:

```c
y = x++;
```

As we have used the increment operation in the postfix form, the value of the variable x will be first assigned to the variable y. Hence, the value of the variable y will be set as 10. After the assignment operation is completed, the value of the variable x will be changed to 11 as shown in Figure 3.20. Hence, it will be correct to say that the postfix form of the increment operator assigns the older value of the variable x to the variable y.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_106_2.png)

**Figure 3.20.** Value of variables x and y

reflect a new value as 11. Hence, the expression to calculate the value of variable r1 can be rewritten as shown below:

```c
r1 = 5 + 10; /* old value of the variable a is used to calculate the result of the expression */
```

Note that, the value of a is considered as 10 for calculating the value of variable r1 because the postfix form of the increment operation always uses the older value of the variable to calculate the result of the expression. Hence, the value of the variable r1 will be evaluated as 15 and then the value of a will be incremented to 11 as shown in Figure 3.22.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_108_0.png)

**Figure 3.22:** Variables r1 and a

The next statement,

```c
r2 = b--;
```

initializes the value of the variable r2 by applying a postfix decrement operator to the variable b. This means that the value of the variable b will be first assigned to the variable r2 following which the value of variable b will be decremented. Hence, the value of variable r2 will be set to 20 following which the value of variable b will be decremented to 19 as shown in Figure 3.23.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_108_1.png)

**Figure 3.23:** Variables r2 and b

The statement,

```c
r3 = --r2;
```

initializes the value of the variable r3 by applying a prefix decrement operator to the variable r2. This means that, the value of the variable r2 will be first decremented to reflect the new value as 19 (since the value of r2 was previously set as 20 as per Figure 3.23) and the new value of r2 will then be assigned to the variable r3. Therefore, the values of the variables r2 as well as r3 will be set to 19 as shown in Figure 3.24.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_109_0.png)

**Figure 3.24:** Variables r2 and r3

The values of variables a, b, r1, r2, and r3 are as shown in the output of the program.

## 3.7 Order of Operations Evaluated by the `printf()` Statement

The `printf()` statement in C evaluates all the operations specified in a direction from right to left (R→L). For example, if ‘op1’ and ‘op2’ are two different operations and if the `printf()` statement is written as below,

```c
printf("control string", op1, op2);
```

then the operation ‘op2’ will be executed before the execution of the operation ‘op1’. This is because, the operation ‘op2’ is the rightmost operation in the `printf()` statement. However, keep a note that the order of printing will still be ‘left to right’ which is exactly opposite to the order of execution. This means that, although the operation ‘op2’ is executed before ‘op1’, the result of operation ‘op1’ will be printed on the computer screen before printing the result of operation ‘op2’.

Therefore, if the `printf()` statement contains a series of increment/decrement operations, the rightmost increment/decrement in the statement will be evaluated before the result of leftmost increment/decrement operator is evaluated. As an example, to understand the order in which the operations inside `printf()` statement are executed, let us determine the output of the code which is as given below:

```c
#include<stdio.h>
void main()
{
    int a=10;
    printf("%d %d %d\n", a++, ++a, --a);
    printf("The last value of a is %d", a);
}
```

### Output

```text
10 10 9
The last value of a is 11
```

The statement,

```c
int a=10;
```

creates an integer type variable named as a with value 10 stored inside it.

The second statement,

```c
printf("%d %d %d\n", a++, ++a, --a);
```

prints the following output on the computer screen:

```text
10 10 9
```

The order in which the increment/decrement operators will be evaluated is from **right to left** whereas the order of printing the result on the computer screen will be from **left to right**. As there is a difference between the order of evaluation and the order of printing, we trace the output of the statement in reverse order as seen in the figures given below.

Firstly, the operation --a will be executed which will decrement the value of variable a to 9 and hence print 9 on the computer screen as shown in Figure 3.25. Note that, the value of variable a is first decremented to store 9 following which it is printed on the screen. This is because we have used the decrement operator in the prefix form as shown in Figure 3.25.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_110_0.png)

**Figure 3.25:** Execution of --a

Secondly, the operation ++a will be executed which will increment the value of variable a to 10 and hence print 10 on the computer screen as shown in Figure 3.26. Note that, the value of variable a is first incremented to store 10 following which it is printed on the screen. This is because we have used the increment operator in the **prefix** form as shown in Figure 3.26.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_111_0.png)

**Figure 3.26:** Execution of ++a

Thirdly, the operation a++ will be executed which will first print the value of variable a which is 10 on the computer screen following which the value of variable a will be incremented to 11 as shown in Figure 3.27. Note that, the old value of variable a is first printed on the screen following which it is incremented in the memory because the increment operator is used in the **postfix** form as shown in Figure 3.27.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_111_1.png)

**Figure 3.27:** Execution of a++
