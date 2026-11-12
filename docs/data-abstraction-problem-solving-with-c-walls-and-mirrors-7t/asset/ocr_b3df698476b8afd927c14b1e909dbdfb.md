# FIGURE A-6 A one-dimensional array of at most seven elements

![](bbox=[0.15, 0.13, 0.75, 0.23])

Clearly, before you access an element of an array, you must assign it a value. You must assign values to array elements one at a time by using the previously described index notation. Note that, if a and b are arrays of the same type, the assignment a = b is illegal.

The data type of maxTemps is a derived type, which is a type that you derive from the fundamental types by using a declaration operator such as []. Naming a derived type by using a typedef is often useful. Thus, you can write

```
const int DAYS_PER_WEEK = 7;
typedef double ArrayType[DAYS_PER_WEEK];
ArrayType maxTemps;
```

and make ArrayType available for use throughout your program.

**Initialization.** You can initialize the elements of an array when you declare it for the first time. For example,

> You can initialize an array when you declare it

```
double maxTemps[DAYS_PER_WEEK] = {82.0, 71.5, 61.8, 75.0, 88.3};
```

initializes the first five elements of maxTemps to the values listed and the last two elements to zero.

**Passing an array to a function.** If you wanted a function that computed the average of the first n elements in a one-dimensional array, you could declare the function as

```
double getAverageTemp(double temperatures[], int n);
```

Because the compiler does not know the number of items that the array can hold, you must also pass the function either the size of the array or the number of array items to process. Traditionally, the array is listed as the first parameter and the number of items as the second. You can invoke the function by writing, for example,

```
double avg = getAverageTemp(maxTemps, 5);
```

where maxTemps is the previously defined array.

> Arrays are always passed by reference to a function

An array is never passed to a function by value, regardless of how you write its parameter. An array is always passed by reference. This restriction avoids copying of perhaps many array entries. Thus, the function getAverageTemp could modify the elements of maxTemps, even though the array is an input to the function. To prevent such alteration, you can specify the array parameter as a constant reference parameter by preceding its type with const, as follows:

```
double getAverageTemp(const double temperatures[], int n);
```