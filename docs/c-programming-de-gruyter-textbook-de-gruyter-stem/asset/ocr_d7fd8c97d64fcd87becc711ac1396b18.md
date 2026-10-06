Execute the function call in the main function:
Swap(x,y)

Inside the function Swap:

| t=a; | | b=t; |
|---|---|---||
| 5 | 10 | 5 | 10 |
| x | y | x | y |

| 5 | 10 | | 5 | 10 |
|---|---|---|---|--|
| a | b | | a | b |
| t | 5 | | t | 5 |

Returned to the main function:
x y

**Fig. 3.4:** The status of variables when the program in Example 3.11 is running.

# Running result:

x=5 y=10
x=5 y=10

Analysis: From the running result we can see that the values of variable x and y have not been swapped. It's because the function call above we use Call-by-Value to pass parameters, only where the values of the actual parameters are passed to the formal parameters. Thus the change of the formal parameters afterwards will not affect the actual parameters. Figure 3.4 shows the status of the variables when the program is running.

# 2. Call-by-Reference

We have seen that passing parameters through Call-by-Value is unidirectional. So how can changes made in the called function on formal parameters affect the actual parameters in the calling function? We can use Call-by-Reference to achieve this.

Reference is a special type of variable; it can be viewed as an alias of another variable. Accessing the reference of a variable is the same as accessing the variable itself. Here is an example: