# 758 Numerical Methods

```
cin >> a >> b;
cout << "Enter the convergence criteria: ";
cin >> epsilon;
cout << "Enter the maximum number of iterations allowed: ";
cin >> imax;
```

```
bisection(a, b, epsilon, imax);
```

```
return 0;
```

```
// A bisection function that finds roots of a function
// The interval a < x is known to contain a root of f(x). The estimate
// of the root is improved successively by finding in which half of the
// interval root lies and then replacing the original interval by that
// half-interval.
```

```
void bisection(double a, double b, double epsilon, int imax)
{
    int i; // current iteration counter
    double x1, x2, x3; // left, right, and midpoint of current interval
    double f1, f2, f3; // function evaluated at these points
    double width; // width of original interval = (b - a)
    double curwidth; // width of current interval = (x3 - x1)
```

```
// echo the passed input data
cout << "\nOriginal search interval is from "
cout << a << " to " << b << endl;
cout << "The convergence criterion is: interval * " << epsilon << endl;
cout << "The maximum number of iterations allowed is * " << imax << endl;
```

```
// calculate the root
x1 = a;
x3 = b;
f1 = f(x1);
f3 = f(x3);
width = (b - a);
```

```
// verify there is a root in the interval
if (f1 * f3 > 0.0)
cout << "\nNo root in the original interval exists" << << endl;
else
{
```

![](bbox=[0.853, 0.867, 0.883, 0.887])