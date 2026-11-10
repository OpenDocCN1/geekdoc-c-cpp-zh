we use x. By the same logic, &signal[2] is also a valid scanf argument like &x. It is easy to cycle through all array elements by using the array subscript as a key variable in a loop.

C doesn’t offer bounds checking for arrays, i.e. it doesn’t validate the index used to access an array element. For instance, the compiler will not generate an error if you attempt to access signal[35] even though the array has 32 elements. A negative index (as in signal[-5]) doesn’t generate an error either. However, these accesses create problems at runtime because the program accesses an area of memory that was not allocated for the array. C trusts the programmer, so you’ll have to do the bounds checking yourself.

The data type of an array is not restricted to the fundamental ones. Even derived and user-defined types like pointers and structures can be stored in arrays. C also supports multi-dimensional arrays where an element is handled with multiple subscripts. Since there is virtually no limit to the number of indexes and dimensions an array can have, arrays in C are very powerful data structures that can easily gobble up a lot of memory.

Because arrays can save a lot of data using a single identifier, there are a number of useful things you can do with them. You can add or delete array elements, reverse an array, sort and search it as well. You can also make a frequency count of the items in an array. Furthermore, many of the routines we develop in this chapter deserve to be converted to functions, a task that we’ll attempt in Chapter 11.

> **Note:** C doesn’t complain if you use a negative index or one that exceeds its size. For instance, `rate[-2]` will clear the compilation phase but it will evaluate to an unpredictable value at runtime. It may destroy another variable, i.e., a part of the program you are running.

# 10.2 DECLARING AND INITIALIZING AN ARRAY

Like a variable, an array has to be declared before use. The declaration of an array specifies its name, type and size, which is normally specified as a constant or symbolic constant. The following statement declares a single-dimensional array named signal having 32 elements, each of type int:

```
int signal[32];  *Size specified explicitly*
```

This declaration also defines the array by allocating the required memory where the last segment of memory is used by signal[31]. The sizeof operator, when used on an array, returns the total usage of all elements, so the above definition allocates 32 × sizeof(int) bytes of memory—typically, 128 bytes. Figure 10.1 depicts the memory layout of a single-dimensional array of 10 elements.

Arrays of other primitive data types are declared in a similar manner:

```
short months[12];  *Unlikely to change size*
float rate[10];
char name[SIZE];  *Uses symbolic constant*
```

The naming rules for variables (5.2.1) apply in identical manner to arrays. This means that the name of an array can comprise only letters, numerals and the underscore character, but it cannot begin with a digit. Also, case is significant, so months[12] and MONTHS[12] are two separate arrays.