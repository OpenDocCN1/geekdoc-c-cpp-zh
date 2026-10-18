7.

```
10 20 30
1 2 3
1 20 3
```

8.

```
Enter two integers: 5 10
In reverse order the numbers are: 5 5
```

different

9.

```
par1Value in function call = 111
par2Ref in function call = 222
n1 after function call = 1
n2 after function call = 2
```

different

10. void zeroBoth(int& n1, int& n2)
{
    n1 = 0;
    n2 = 0;
}

11. void addTax(double taxRate, double& cost)
{
    cost = cost + ( taxRate/100.0 ) * cost;
}

The division by 100 is to convert a percent to a fraction. For example, 10% is 10/100.0 or 1/10th of the cost.

12. Yes, a function that returns a value can have a call-by-reference parameter. Yes, a function can have a combination of call-by-value and call-by-reference parameters.

13. No, a function definition cannot appear inside the body of another function definition.

14. Yes, a function definition can contain a call to another function.

15. void order(int& n1, int& n2);
//Precondition: The variables n1 and n2 have values.
//Postcondition: The values in n1 and n2 have been
//ordered so that n1 <= n2.

16. double sqrt(double n);
//Precondition: n >= 0.
//Returns the squareroot of n.

You can rewrite the second comment line to the following if you prefer, but the previous version is the usual form used for a function that returns a value:

//Postcondition: Returns the squareroot of n.