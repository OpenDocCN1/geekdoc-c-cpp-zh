
## Program 5.8 Use of a flag (Continued)

| Run: |
|---|
| The number is: 170 |
| Run: |
| The number was not found! |

Note that we test the program with the same file and two different contents. In the first run, the contents of the file is

90 110 120 135 **170** 200 230 **EOF**

We come out of the loop when 170 is read because it matches the condition we are looking for (it is greater than 150). The flag is set to *true*, which means !flag is *false* and the loop is terminated although the other condition (infile >> num) is *true*. In the second run the contents of the file is

90 110 120 135 137 140 **EOF**

The flag never becomes *true*, but when we reach the EOF, the other condition (*infile >> num*) becomes *false* and the loop is terminated. If the number is found inside the loop, we print it. If the loop is terminated, the flag is still *false* and we know that we have reached the end of file.

## Pitfalls

Although there are many pitfalls to be avoided with the *while* statement, we mention only four here.

### Zero-Iteration Loop

We must avoid a loop that never iterates. This happens when the Boolean expression is *false* when it is tested for the first time. In this case, the body of the loop never executes no matter how many times we run the program. Unfortunately, this problem is not caught during compilation-time or run-time. We must be very careful to avoid this situation. The following are two cases of zero iteration.

```cpp
while (false)                 while (2 == 3)
{
    ...                         ...
}
```

### Infinite-Iteration Loop

Another example of a *while* statement pitfall is a loop that repeats its body forever. This happens when the Boolean expression is *true* each time it is tested. In this case, the loop never stops. This type of a loop should normally be avoided, but, as we will discuss in the next section, we create such a loop to let a server program run forever.

```cpp
while (true)                 while (2 != 3)
{                            {
    ...                          ...
}                            }
```

### Empty-Body Loop

Sometimes we accidentally create a loop whose body is empty. This happens, for example, if we add a semicolon after the header of the `while` statement. The compiler thinks that we do not want to use braces and that there is a null statement before the semicolon. The actual body is interpreted as a stand-alone statement that is executed once after the loop. The compiler does not give an error, but the program does not do what we expected (logical error).

```cpp
while (expression); // Empty statement (compound statement ignored)
{
    ...
}
```

### Use of Floating-Point Values in Boolean Expressions

As we discuss in a previous chapter, floating-point values depend on the precision of the numbers in any system. For example, 3.141516 and 3.1415 are not equal but may appear to be equal if the precision is only four places after the decimal point. For this reason, we must be very careful when testing floating-point numbers for equality.

## Creating a Delay

C++ provides several tools (discussed in future chapters) to create a delay in a program. We can also create a delay using a `while` statement. We can use a counter-controlled `while` statement whose body has only the updating statement. The loop does not do anything but go through iterations, which creates a delay. The following is an example. The code creates a 10-second delay if the computer performs 10,000 iterations in a second, which means this type of delay depends on the speed of the computer.

```cpp
int counter = 0;
while (counter < 100000)
{
    counter++;
}
```

## 5.2.3 Analysis of a *while* Statement

We can better understand the behavior of the `while` statement if we think of it as a combination of decision-making statements as shown in Figure 5.10. In each loop execution, there is a *true path* and a *false path*. Figure 5.10 shows that the number of tests is always one more than the number of repetitions. If the body of the loop is repeated *n* times, *n* + 1 tests are made. In the first *n* tests, the result is *true*; in the last test, the result is *false*. This means that even if the body is not executed at all, we need to make one test and the result should be *false*. The above analysis shows that the `while` statement is a **pre-test loop**. A test must be done in each iteration before the body is executed.

![](img/d68f6199646ca63591a6d8419e0ed4ba_193_0.png)

| Statistics |  |
|---|---|
| Repetition | *n* |
| Testing | *n* + 1 |

The testing result should be the same in the last test: false.

**Figure 5.10**  Analysis of a *while* statement

> **A while statement is a pre-test loop.**  
> If the body is executed *n* times,  
> the condition has been tested (*n* + 1) times.

## 5.3 THE *for* STATEMENT

As we discussed in the previous section, we can always use the `while` statement as a counter-controlled loop. C++ provides another loop construct, however, called the *for* statement, that is particularly useful when we need counter-controlled iteration. It combines the three elements of a loop—initialization, conditional test, and update—into the loop construct itself. A quick comparison between the two loops shows that the *for* statement is much more compact than using a *while* statement for counter-controlled looping, as shown in Figure 5.11.

### 5.3.1 Header

We now discuss in detail each of the three sections in the header of a *for* statement.

![](img/d68f6199646ca63591a6d8419e0ed4ba_193_1.png)

**Figure 5.11**  Comparison between a *while* loop and a *for* loop

### Initialization

The initialization section is an expression that initializes the counter. It is customary to use lowercase variables such as i, j, k, for the counter. We can declare the counter before the header of the loop or declare the counter at the same time that we initialize it.

| // Counter declaration before the header | // Counter declaration inside the header |
| :--- | :--- |
| `int i;`<br>`for (i = 0 ; ... ; ... )`<br>`{`<br>`  actions`<br>`}` | `for (int i = 0 ; ... ; ... )`<br>`{`<br>`  actions`<br>`}` |

In the first method, the scope of the counter extends beyond the boundary of the loop; in the second method, the scope of the counter is only inside the loop.

### Condition

The condition section is the second part in the header. As in the *while* statement, the condition in the *for* statement is a Boolean expression. If the condition is true, the body of the loop is executed; otherwise, the loop exits, which indicates that the *for* statement is a pre-test loop. If the condition section is empty (between the first and the second semicolons), it is defaulted to true.

> If the condition section is empty, it is defaulted to true.

### EXAMPLE 5.11

The following *for* loop does not compile because the condition section in the header is missing.

```cpp
for (int i = 0 ; i++) {...}
```

### EXAMPLE 5.12

The following *for* loop compiles and creates an infinite loop because the condition section is empty and is defaulted to true.

```cpp
for (int i = 0 ; ; i++) {...}
```

### Updating

The updating section is executed after the body of the loop is executed. After updating, the condition is tested again to see if the body should be executed once more. The updating section can be missing, which means updating, explicitly or implicitly, must be done in the body of the loop.

### 5.3.2 Body

The body of the *for* statement should be the same as the body of the corresponding *while* statement with one exception: the updating of the counter is missing because it has been moved to the header.

### EXAMPLE 5.13

We can change Program 5.3, which used a *while* statement, to Program 5.9, which uses a *for* statement. We can see that the result is the same, but the *for* statement makes the program shorter and easier to understand.
