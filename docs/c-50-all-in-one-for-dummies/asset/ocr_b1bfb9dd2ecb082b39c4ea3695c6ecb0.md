Array is a structure that can contain a series of elements of the same type (all int values and all double values, for example, or all Vehicle objects and Motor objects — you meet these latter sorts of objects in Chapter 7 of this minibook).

# The argument for the array

Consider the problem of averaging a set of six floating-point numbers. Each of the six numbers requires its own double storage:

```
double d0 = 5;
double d1 = 2;
double d2 = 7;
double d3 = 3.5;
double d4 = 6.5;
double d5 = 8;
```

(Averaging int variables can result in rounding errors, as described in Chapter 2 of this minibook.)

Computing the average of those variables might look like this:

```
double sum = d0 + d1 + d2 + d3 + d4 + d5;
double average = sum / 6;
```

Listing each element by name is tedious. Okay, maybe it’s not so tedious when you have only 6 numbers to average, but imagine averaging 600 (or even 6 million) floating-point values.

# The fixed-value array

Fortunately, you don’t need to name each element separately. C# provides the array structure that can store a sequence of values. Using an array, you can put all your doubles into one variable, like this:

```
double[] doublesArray = {5, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3};
```

You can also declare an empty array without initializing it:

```
double[] doublesArray = new double[6];
```

This line allocates space for six doubles but doesn’t initialize them.

The Array class, on which all C# arrays are based, provides a special syntax that makes it more convenient to use. The paired brackets [] refer to the way you access individual elements in the array:

```
doublesArray[0] // Corresponds to d0 (that is, 5)
doublesArray[1] // Corresponds to d1 (that is, 2)
```

![](bbox=[0.13, 0.8, 0.22, 0.92])