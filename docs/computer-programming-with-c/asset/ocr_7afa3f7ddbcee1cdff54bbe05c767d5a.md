![](bbox=[0.12, 0.11, 0.86, 0.365])

**Figure 2.32:** Printing the value of a variable using cout statement

part of the message is the name of the variable (variable a) which is not surrounded in the double quotes. Further, it is important to note that we must use the insertion operator separately so as to insert every part of the message on the computer screen. The working of the cout statement is shown in Figure 2.33.

![](bbox=[0.12, 0.52, 0.86, 0.68])

**Figure 2.33:** Execution of `cout<<"The value of variable is "<<a;`

As an example, let us consider that x and y are variables of type integer with a value of 10 and 20 as shown below:

```
```cpp
int x=10,y=20;
```
```

Similarly, the cout statement,

```
```cpp
cout<<"Value of x is:"<<x<<" Value of y is:"<<y;
```
```

will print the following message on the computer screen.

```
```text
Value of x is:10 Value of y is:20
```
```