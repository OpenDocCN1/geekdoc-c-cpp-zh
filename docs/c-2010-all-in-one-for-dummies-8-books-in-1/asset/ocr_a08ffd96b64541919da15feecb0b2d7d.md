# A Loop made foreach Array 115

named Length that contains its length. doublesArray.Length has the same value as numElements.

The following for loop is preferable:

```
// Accumulate the values into an array.
for (int i = 0; i < doublesArray.Length; i++) ...
```

# Initializing an array

The following lines show an array with its initializer and then one that allocates space but not initialize the elements' values:

```
double[] fixedLengthArray = (5, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3);
double[] = new double[10];
```

You can do it using the following code:

```
double[] fixedLengthArray = new double[10] (5, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3);
```

Here, you have specifically allocated the memory new and then declared with the initial values for the members of the array. I think I can predict what form you prefer. (Hint: Line 1?)

# A Loop made foreach Array

Given an array of strings, the following loop averages its lengths:

```
public class Student // Read about classes in Book II.
{
    public string name; // Grade point average
    public double gpa;
}
public class Program
{
    public static void Main(string[] args)
{
        // . create the array somehow . .
        // Now average the students you have.
        double sum = 0.0;
        for (int i = 0; i < students.Length; i++)
        {
            sum += students[i].gpa;
            double avg = sum / students.Length;
            // . do something with the average . . .
        }
}
```

The for loop iterates through the members of the array. (Yes, you can have arrays of any sort of object, not just of simple types as double and string. You likely haven't been formally introduced to classes yet, so bear with me a bit longer. I get into them in the next book.)