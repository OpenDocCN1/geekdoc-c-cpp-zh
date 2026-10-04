of the array. (Iterate means to loop through the array one element at a time, as with a for loop.)

It would be a shame and a crime to have to schlep around the variable numElements with doublesArray everywhere it goes just so that you know how long it is. Fortunately, that isn’t necessary. An array has a property named Length that contains its length. doublesArray.Length has the same value as numElements.

The following for loop is preferable:

```
// Accumulate the values into an array.
for (int i = 0; i < doublesArray.Length; i++) ...
```

# Initializing an array

The following lines show an array with its initializer and then one that allocates space but doesn’t initialize the elements’ values:

```
double[] fixedLengthArray = {5, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3};
double[] variableLengthArray = new double[10];
```

You can do it all yourself using the following code:

```
double[] fixedLengthArray = new double[10] {5, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3};
```

Here, you have specifically allocated the memory using new and then followed that declaration with the initial values for the members of the array. I think I can predict which form you prefer. (Hint: Line 1?)

# A Loop Made for each Array

Given an array of strings, the following loop averages their lengths:

```
public class Student  // Read about classes in Book II.
{
    public string name;
    public double gpa;        // Grade point average
}
public class Program
{
    public static void Main(string[] args)
    {
        // ...create the array somehow ...
        // Now average the students you have.
        double sum = 0.0;
        for (int i = 0; i < students.Length; i++)
        {
            sum += students[i].gpa;
        }
        double avg = sum / students.Length;
        // ...do something with the average ...
    }
}
```