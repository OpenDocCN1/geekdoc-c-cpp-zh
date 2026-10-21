```
return 0;
}

double& lowest(double a[], int len)
{
    int j = 0;                         // Index of lowest element
    for(int i = 1; i < len; i++)
        if(a[j] > a[i])                // Test for a lower value...
            j = i;                     // ...if so update j
    return a[j];                       // Return reference to lowest
                                   // element
}
```

The output from this example is:

```
3   10   1.5   15   2.7   23   4.5   12   6.8   13.5   2.1   14
3   10   6.9   15   2.7   23   4.5   12   6.8   13.5   7.9   14
```

# How It Works

Let’s first take a look at how the function is implemented. The prototype for the function lowest() uses double& as the specification of the return type, which is therefore of type ‘reference to double’. You write a reference type return value in exactly the same way as you have already seen for variable declarations, appending the & to the data type. The function has two parameters specified — a one-dimensional array of type double and a parameter of type int that specifies the length of the array.

The body of the function has a straightforward for loop to determine which element of the array passed contains the lowest value. The index, j, of the array element with the lowest value is arbitrarily set to 0 at the outset, and then modified within the loop if the current element, a[i], is less than a[j]. Thus, on exit from the loop, j contains the index value corresponding to the array element with the lowest value. The return statement is as follows:

```
return a[j];                     // Return reference to lowest element
```

In spite of the fact that this looks identical to the statement that would return a value, because the return type was declared as a reference, this returns a reference to the array element a[j] rather than the value that the element contains. The address of a[j] is used to initialize the reference to be returned. This reference is created by the compiler because the return type was declared as a reference.

Don’t confuse returning &a[j] with returning a reference. If you write &a[j] as the return value, you are specifying the address of a[j], which is a pointer. If you do this after having specified the return type as a reference, you get an error message from the compiler. Specifically, you get this:

```
error C2440: 'return' : cannot convert from 'double * __w64 ' to 'double &'
```

The function main(), which exercises the lowest() function, is very simple. An array of type double is declared and initialized with 12 arbitrary values, and an int variable len is initialized to the length of the array. The initial values in the array are output for comparison purposes.

> Again, the program uses the stream manipulator setw() to space the values uniformly, requiring the #include directive for <iomanip>.