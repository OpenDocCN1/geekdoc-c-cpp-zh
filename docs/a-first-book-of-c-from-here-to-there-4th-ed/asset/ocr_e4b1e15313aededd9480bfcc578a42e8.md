# Chapter 6

Because the value of more than one variable is affected, swap() can’t be written as a pass by value function that returns a single value. The exchange of main()’s variables by swap() can be accomplished only by giving swap() access to main()’s variables. One way of doing this is using reference parameters.

You have already seen how to pass references to two variables in Program 6.8. Now you see how to construct a function to exchange the values in the passed reference parameters. Exchanging values in two variables is done with this three-step exchange algorithm:

+   1. Save the first parameter’s value in a temporary location (see Figure 6.9a).

![](bbox=[0.308, 0.292, 0.759, 0.365])

**Figure 6.9a**  Save the first value

+   2. Store the second parameter’s value in the first variable (see Figure 6.9b).

![](bbox=[0.309, 0.453, 0.759, 0.525])

**Figure 6.9b**  Replace the first value with the second value

+   3. Store the temporary value in the second parameter (see Figure 6.9c).

![](bbox=[0.31, 0.601, 0.759, 0.699])

**Figure 6.9c**  Change the second value

Following is the swap() function written according to these specifications:

```
void swap(double& num1, double& num2)
{
    double temp;

    temp = num1;     // save num1's value
    num1 = num2;     // store num2's value in num1
    num2 = temp;     // change num2's value

    return;
}
```