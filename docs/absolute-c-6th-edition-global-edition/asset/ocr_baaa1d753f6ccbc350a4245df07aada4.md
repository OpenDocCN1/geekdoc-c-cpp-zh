+   3. 10 20 30
+   1 2 3
+   1 20 3

+   4. Enter two integers: 5 10
+   In reverse order the numbers are: 5 5

```
5. void zeroBoth(int& n1, int& n2)
{
    n1 = 0;
    n2 = 0;
}
```

```
6. void addTax(double taxRate, double& cost)
{
    cost = cost + (taxRate/100.0)*cost;
}
```

The division by 100 is to convert a percentage to a fraction. For example, 10% is 10/100.0, or one-tenth of the cost.

+   7. par1Value in function call = 111
+   par2Ref in function call = 222
+   n1 after function call = 1
+   n2 after function call = 2

8. The one with one parameter would be used because the function call has only one parameter.

9. The first one would be used because it is an exact match, namely, two parameters of type double.

10. This cannot be done (at least not in any nice way). The natural ways to represent a square and a round pizza are the same. Each is naturally represented as one number, which is the radius for a round pizza and the length of a side for a square pizza. In either case the function unitPrice would need to have one formal parameter of type double for the price and one formal parameter of type int for the size (either radius or side). Thus, the two function declarations would have the same number and types of formal parameters. (Specifically, they would both have one formal parameter of type double and one formal parameter of type int.) Thus, the compiler would not be able to decide which definition to use. You can still defeat this evil pizza parlor's strategy by defining two functions, but they will need to have different names.

11. The fundamental rule for testing functions is that every function should be tested in a program in which every other function in that program has already been fully tested and debugged. This is a good way to test a function because if you follow this rule, then when you find a bug, you will know which function contains the bug.

12. A driver program is a program written for the sole purpose of testing a function.

13. A stub is a simplified version of a function that is used in place of the function so that other functions can be tested.