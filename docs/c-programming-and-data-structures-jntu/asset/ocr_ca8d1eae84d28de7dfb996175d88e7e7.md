A self-contained and independent function should behave like a 'black box' that receives a predefined form of input and outputs a desired value. Such functions will have two-way data communication as shown in Fig. 10.8.

We shall modify the program in Fig. 10.7 to illustrate the use of two-way data communication between the calling and the called functions.

![](bbox=[0.2, 0.29, 0.8, 0.43])

Fig. 10.8 Two-way data communication between functions

# Example 10.3

In the program presented in Fig. 10.7, modify the function value, to return the final amount calculated to the main, which will display the required output at the terminal. Also extend the versatility of the function println by having it to take the length of the line as an argument.

The modified program with the proposed changes is presented in Fig. 10.9. One major change is the movement of the printf statement from value to main.

The calculated value is passed on to main through the statement:

```
return(sum);
```

The integer value of sum at this point is returned to main and assigned to the variable amount by the function call

```
amount = value(principal,inrate,period);
```

The following events occur, in order, when the above function call is executed:

+   1. The function call transfers the control along with copies of the values of the actual arguments to the function value where the formal arguments p, r, and n are assigned the values of principal, inrate, and period respectively.
+   2. The called function value is executed line by line in a normal fashion until the return(sum); statement is encountered. At this point, the value of sum is passed back to the function-call in the main and the following indirect assignment occurs:

```
value(principal,inrate,period) = sum;
```

```
Program
/* ************************************************************ */
/* FUNCTIONS WITH ARGUMENTS AND RETURN VALUES */
/* ************************************************************ */
main()
{
  float principal, inrate, amount;
  int period;
```