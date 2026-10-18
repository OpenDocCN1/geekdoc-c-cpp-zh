4. In the template prefix

```
template<class T>
```

what kind of variable is the parameter T?

+   a. T must be a class.
+   b. T must not be a class.
+   c. T can be only types built into the C++ language.
+   d. T can be any type, whether built into C++ or defined by the programmer.

# Algorithm Abstraction

As we saw in our discussion of the swapValues function, there is a very general algorithm for interchanging the value of two variables, and this more general algorithm applies to variables of any type. Using a function template, we were able to express this more general algorithm in C++. This is a very simple example of algorithm abstraction. When we say we are using algorithm abstraction, we mean that we are expressing our algorithms in a very general way so that we can ignore incidental detail and concentrate on the substantive part of the algorithm. Function templates are one feature of C++ that supports algorithm abstraction.

# PROGRAMMING EXAMPLE

# A Generic Sorting Function

In Chapter 7 we gave a simple sorting algorithm to sort an array of values of type int. The algorithm was realized in C++ code as the function sort, which we gave in Display 7.12. Here we repeat the definition of this function sort:

```
void sort(int a[], int numberUsed)
{
    int indexOfNextSmallest;
    for (int index = 0; index < numberUsed - 1; index++)
    {//Place the correct value in a[index]:
        indexOfNextSmallest =
            indexOfSmallest(a, index, numberUsed);
        swapValues(a[index], a[indexOfNextSmallest]);
        //a[0] <= a[1] <=...<= a[index] are the smallest of
        //the original array elements. The rest of the
        //elements are in the remaining positions.
    }
}
```

If you study this definition of the function sort, you will see that the base type of the array is never used in any significant way. If we replace the base type of the array in the function header with the type double, then we would obtain a sorting function that applies to arrays of values of type double. Of