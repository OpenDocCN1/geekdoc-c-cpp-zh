```
```cpp
traceMe(one, two);
traceMe(two, one);

return 0;
}

void traceMe(double x, double y)
{
    double z;

    if (x != 0)
        z = sqrt(y) / x;
    else
    {
        cout << "Enter a nonzero number: ";
        cin >> x;
        cout << endl;
        z = floor(y, x);
    }

    cout << fixed << showpoint << setprecision(2);
    cout << x << ", " << y << ", " << z << endl;
}
```
```

+   a. What is the output if the input is 3 625?
+   
+   b. What is the output if the input is 24 1024?
+   
+   c. What is the output if the input is 10 196?

31. The function traceMe in Exercise 30 outputs the values of x, y, and z. Modify the definition of this function so that rather than print these values, it sends the values back to the calling environment and the calling environment prints these values.

32. In Exercise 30, determine the scope of each identifier.

33. What is the output of the following code fragment? (Note: alpha and beta are int variables.)

```
```cpp
alpha = 5;
beta = 10;

if (beta >= 10)
{
    int alpha = 10;
    beta = beta + alpha;
    cout << alpha << " " << beta << endl;
}

cout << alpha << " " << beta << endl;
```
```