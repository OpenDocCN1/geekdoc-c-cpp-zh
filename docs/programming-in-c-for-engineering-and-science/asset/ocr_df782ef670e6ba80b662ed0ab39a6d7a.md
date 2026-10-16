```
else
{
    cout << "Illegal scale: " << toScale << " -- returning 0\n";
    return 0;
}
```

Suppose that celsConverter() is called with scale as an argument,
cout << celsConverter(100.0, scale) << endl;

where scale is a string variable whose value is "Kelvin". Before celsConverter() can begin execution, two actions must occur:

+   1. Sufficient space must be allocated for the parameter toScale to hold its argument:

![](bbox=[0.05, 0.39, 0.45, 0.53])

+   2. The argument must be copied into this space:

![](bbox=[0.05, 0.63, 0.45, 0.77])

In this example, six characters must be copied into the parameter's space and if the argument's value were "Fahrenheit", ten characters would need to be copied. Such copying takes time, increasing the execution time of the function. In general, if a parameter whose type is a class is a value parameter, then the members of the corresponding class argument must be copied, which can be time-inefficient.

# 10.2.3.2 A Danger with Reference Parameters

Call by reference does not suffer this time-inefficiency because a reference parameter is an alias for its argument—no copying is required. To avoid the time-consuming copying of values required by call-by-value, many programmers in languages other than C++ always pass large arguments by reference, regardless of whether their movement is into or out of the function. To illustrate, suppose we make toScale a reference parameter in the function celsConverter():

```
double celsConverter(double degrees, string &toScale)
```