# Chapter 13 Underlying C Language Features

# Is It an Array, or Is It a Pointer? you simply specify the name of the array, as you did previ-

To pass an array to a function, you simply ousvi-sly with the call to the arraySum function. But we also mentioned in this section that to produce a pointer to an array, you only need specify the name of the array. This implies that in the call to the arraySum function, a pointer to the array values was passed to the function. This is precisely the case and explains why you can change the elements of an array from within a function.

But if a pointer to the array is passed to the function, which isn't the formal parameter inside the function declared to be a pointer? In words, in the declaration of array in the arraySum function, why isn't this declared?

```
*array;
```

Shouldn't all references to an array within a function be made using pointer variables?

To answer these questions, we must first reiterate what we have already said about point- ers and arrays. We mentioned that if valuesPtr to the same type of element as contained in an array called values, the expression *(valuesPtr + i) is equivalent to the expression values[i],assuming that valuesPtr has been set to the beginning of values.What follows from this is that you can use the expression *(values - i) to reference the i-th element of the array values—and, in general, if x is an array of any type, the expression x[i] can always be equivalently expressed in Objective-C as *(x - i).

As you can see, pointers and arrays are intimately related in Objective-C, which is why you can declare array to be of type "array of int" inside the arraySum function or to be of type "pointer to int." Either declaration works fine in the preceding program—try it and see.

If you will use index numbers to reference the elements of an array, declare the corresponding formal parameter to be array. This more correctly reflects the function's use of array. Similarly, if you will be using the argument as a pointer to the array, declare it to be of pointer type.

# Pointers to Character Strings

One of the most common applications of using a pointer to an array is as a pointer to a character string. The reasons are of not convenience and efficiency. To show how easily you can use pointers to character strings, let's write a function copyString to copy one string into another. If you were writing this function using your normal array-indexing methods, you might code the function as follows:

```
void copyString(char to[], char from[])\{
  int i;

  for ( i = 0; from[i] != '\0'; ++i )
    to[i] = from[i];
n}
```