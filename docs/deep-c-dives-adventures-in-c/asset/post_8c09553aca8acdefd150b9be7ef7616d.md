
Notice that as we are using the simpler SMF, the first element is:
`myArray[0]`
and the last is:
`myArray[9]`

This mismatch between the number of elements and the index of the last element is something that really bothers beginners who often, incorrectly, think that:
`int myArray[10];`
means that the last element is `myArray[10]`. It is also the reason that for loops that process the entire array are written to stop at *number-1*, rather than *number*. To avoid both of these confusions some languages, Basic for example, work with arrays that use 1 as the start rather than 0.

## Arrays Are Pointers

In other languages the distinction between an array and something you might construct using an SMF is deeply hidden in an effort to make the language as high-level as possible, but C isn't a high-level language. In C we make a point of an array being a pointer.

In C the instruction:
`int temp = myArray[0];`
is equivalent to:
`int temp = *myArray;`

The variable that represents the array is a pointer and can be used with either indexing or dereferencing. In fact, any pointer can be used with indexing and, in this sense, not only is every array a pointer, but every pointer is an array. For example:
`int *myPointer = myArray;`
`myPointer[1] = 42;`

`myPointer` isn't declared as an array and yet you can use array index syntax to access an element as if it was an array.

Notice that arrays aren't completely like pointers. Unlike a pointer, the array name isn't a variable and as such cannot be modified. For example;
`myArray = myPointer;`
is illegal. In this respect, arrays are more like constant pointers.

Another important difference between an array and a pointer is the way *sizeof* works. In the case of an array *sizeof* returns the number of elements in the array, whereas in the case of a pointer *sizeof* returns the size of the pointer, typically four bytes, and not the number of elements that it points at. This is a difference imposed by the compiler in that it "knows" the size of the array at compile time and adjusts sizeof accordingly. If you pass an array into a function then the array is treated as a pointer - it is said to “decay” to a pointer, but really all that happens is that the compiler loses track of the fact that it is an array and sizeof returns the size of a pointer. These idiosyncrasies are imposed as an attempt to make arrays behave more like you would expect them to.

Some programmers are very firm in their opinion that an array is not a pointer and, as long as you can see that point of view, you are safe to understand that pointers and the SMF are the basis of the C array.

## Pointer Arithmetic

The fact that pointers are arrays and arrays pointers leads us to implement pointer arithmetic in a very particular way.

Let’s ask, what is the pointer equivalent of:

```
myPointer[5] = 42;
```

If `myPointer` references the start of the array then, using the SMF idea, we can see that `myPointer[5]` is the same as:

```
myPointer + 5*sizeof(int)
```

To make this simpler pointer arithmetic is defined as:

```
myPointer + 5 = myPointer + 5*sizeof(int)
```

where the compiler takes care of multiplying by the size of the element type. That is, in general:

```
myPointer + i = myPointer + i* sizeof(*myPointer)
```

When you add or subtract from a pointer the arithmetic is done in units of the size of the type that is referenced.

Notice that you can apply pointer arithmetic to an array name. For example:

```
myArray + 5;
```

is exactly the same as:

```
myArray[5];
```

but recall that `myArray` behaves more like a constant pointer and you cannot assign to it.

## Pointer to Array

There is a subtle difference in C between a pointer to a type and a pointer to an array of the type. In the first case the pointer references the type and pointer arithmetic moves the reference on by the size of the type. This makes the pointer suitable for the implementation of an array of the type.

Compare this to the idea of a pointer to an array of the type. This was introduced in C89. It is the array of the type that is the fundamental element that the pointer references. If you now add one to the pointer, then it moves on, not by the size of the type, but the size of the array – as the array is the element.

If you write:

```
int *myPointer;
```

then `myPointer` references an integer and adding 1 to it moves it on by the sizeof int. This makes it a way of implementing an array of int.

![](img/5f2ea21c2077d473344a0fdf144677b9_123_0.png)

Compare this to:

```
int (*myPointer) [5];
```

which declares a pointer to an array, each element of which is an array of five ints.

![](img/5f2ea21c2077d473344a0fdf144677b9_123_1.png)

It is a strange notation and probably would be better if it was written:

```
int[5] *myPointer;
```

but it isn’t. The type “pointer to array of five ints” is written `int (*) [5]` which is the form you would use in a cast.

The difference is that now when you add 1 to `myPointer` it moves on by five times the size of int, i.e. 20. Notice that this is the array equivalent of creating a pointer to a struct and it clearly has something to do with multidimensional arrays, see later and Dive 11.

## Casting Pointers

Pointer arithmetic is all about implementing the storage mapping function for the array using pointers and, in most cases, this is exactly what you want. Just occasionally, however, you need to access parts of a data type rather than the whole thing and to do this you need a pointer that points “inside” the data, not just at the start.

For example, suppose you want to access the individual bytes that make up an int. Getting a pointer to the int is easy, but as it is an int pointer adding one to it moves it on by four bytes. If you only want to move it on by a single byte you need to use a cast:

```
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv)
{
    int myVar = 0x01020304;
    char *myPointer = (char *)&myVar;
    printf("%d\n", *(myPointer+1));
    return 0;
}
```

By casting the address to a char pointer adding 1 really does only add 1. You can do this on a temporary basis by casting the pointer:

```
int *myPointer=&myVar;
printf("%d\n", *(char *)myPointer+1);
```

Of course, what you actually see displayed depends on the byte order – big or little endian. For more complex data structures, the exact layout in memory makes a difference.

## More Than One Dimension

If you know about arrays then you will also know that they come in different shapes. The sort of array that we have been looking at is usually called “one-dimensional” or a “vector” because it has only a single index. You can have an array that has more than one index. A two-dimensional array has two and it is generally thought of as a table of rows and columns or as a matrix. For three dimensions we have a cube and beyond this things become difficult, if not impossible, to imagine.

Higher-dimensional arrays are often called “tensors”, but this name comes from physics and math. As far as programming is concerned, an n-dimensional array is simply an array which accepts n indices to identify an element.

Some languages have special syntax for defining multi-dimensional arrays, but C just reapplies the basic array principle as many times as required. The point is that a two-dimensional array is a one-dimensional array where each element is a one-dimensional array. If you want to think in terms of the rows and columns of a matrix, then the C array is a one-dimensional array of rows. This is generally called row-major order as opposed to column-major order used by Fortran, Octave and so on.

The syntax to create a two-dimensional array follows from this description:
`int myArray[5][6];`
which creates an array with 5 rows, each one consisting of an array of 6 ints – the columns.

![](img/5f2ea21c2077d473344a0fdf144677b9_125_0.png)

You can think of this as creating a one-dimensional array where each element is in itself an array of 6 ints.

![](img/5f2ea21c2077d473344a0fdf144677b9_125_1.png)

`int myArray[5][6];` can be thought of as `int[6] myArray[5]`, i.e. an array of five elements each of which is an `int[6]`. Of course, this isn’t valid C - it is just intended to give you some idea of why the syntax is as it is.

Accessing an element of an array also follows the “double index” pattern:
`myArray[i][j]`
refers to the element in the ith row and the jth column. Again it takes the form of the jth element of the array that is the ith element.
