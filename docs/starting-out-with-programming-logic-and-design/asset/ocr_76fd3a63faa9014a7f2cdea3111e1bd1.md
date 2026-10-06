# 3.4 Passing Arguments to Modules

```
5 Module doubleNumber(Integer value)
6 Declare Integer result
7 Set result = value * 2
8 Display result
9 End Module
```

# Program Output

8

When this program runs, the main module will begin executing. The statement in line 2 calls the doubleNumber module. Notice that the number 4 appears inside the parentheses. This is an argument that is being passed to the doubleNumber module. When this statement executes, the doubleNumber module will be called with the number 4 copied into the value parameter variable. This is shown in Figure 3-12.

# Figure 3-12 The argument 4 is copied into the value parameter variable

![](bbox=[0.265, 0.437, 0.725, 0.576])

Let's step through the doubleNumber module. As we do, remember that the value parameter variable will contain the number that was passed into it as an argument. In this program, number is 4.

Line 6 declares a local variable named result. Then, line 7 assigns the value of the expression value * 2 to result. Because the value variable contains 4, this line assigns 8 to result. Line 8 displays the contents of the result variable. The module ends at line 9.

For example, if we had the module as follows:

```
Call doubleNumber(5)
module would have displayed 10.
```

We can also pass the contents of a variable as an argument. For example, look at Program 3-6. The main module declares an Integer variable named number in line 2. Lines 3 and 4 prompt the user to enter a number, and line 5 reads the user's input into the number variable. Notice that in line 6 number is passed as an argument to the