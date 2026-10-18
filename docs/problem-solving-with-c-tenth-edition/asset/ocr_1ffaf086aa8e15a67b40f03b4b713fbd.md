```
int z = power(2, 1);
```

Larger numbers for the second argument will produce longer chains of recursive calls. For example, consider the statement

```
cout << power(2, 3);
```

The value of power(2, 3) is calculated as follows:

```
power(2, 3) is power(2, 2) * 2
power(2, 2) is power(2, 1) * 2
power(2, 1) is power(2, 0) * 2
power(2, 0) is 1 (stopping case)
```

When the computer reaches the stopping case, power(2,0), there are three suspended computations. After calculating the value returned for the stopping case, it resumes the most recently suspended computation to determine the value of power(2,1). After that, the computer completes each of the other suspended computations, using each value computed as a value to plug into another suspended computation, until it reaches and completes the computation for the original call, power(2,3). The details of the entire computation are illustrated in Display 14.4.

# DISPLAY 14.4 Evaluating the Recursive Function Call power(2, 3)

![](bbox=[0.2, 0.52, 0.8, 0.88])