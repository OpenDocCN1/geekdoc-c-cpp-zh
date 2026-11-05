# 1. Introduction

The following example creates an array of int elements, initializes the array, and prints out the contents of the array.

```
using System;
class Test
{
    static void Main() {
        int[] a = new int[10];
        for (int i = 0; i < a.Length; i++) {
            a[i] = 1 + i;
        }
        for (int i = 0; i < a.Length; i++) {
            Console.WriteLine("[a[{0}]] = {1}", i, a[i]);
        }
    }
}
```

This example creates and operates on a single-dimensional array. C# also supports multi-dimensional arrays. The number of dimensions of an array type, also known as the rank of the array type, is one plus the number of commas written between the square brackets of the array type. The following example allocates one-dimensional, two-dimensional, and three-dimensional arrays.

```
int[] a1 = new int[10];
int[,] a2 = new int[10, 5];
int[,,] a3 = new int[10, 5, 2];
```

The a1 array contains 10 elements, the a2 array contains 50 (10 × 5) elements, and the a3 array contains 100 (10 × 5 × 2) elements.

> BILL WAGNER An FxCop rule recommends against multi-dimensional arrays; it's primarily guidance against using multi-dimensional arrays as sparse arrays. If you know that you really are filling in all the elements in the array, multi-dimensional arrays are fine.

The element type of an array can be any type, including an array type. An array with elements of an array type is sometimes called a jagged array because the lengths of the element arrays do not all have to be the same. The following example allocates an array of arrays of int:

```
int[][] a = new int[3][];
a[0] = new int[10];
a[1] = new int[5];
a[2] = new int[20];
```

The first line creates an array with three elements, each of type int[] and each with an initial value of null. The subsequent lines then initialize the three elements with references to individual array instances of varying lengths.