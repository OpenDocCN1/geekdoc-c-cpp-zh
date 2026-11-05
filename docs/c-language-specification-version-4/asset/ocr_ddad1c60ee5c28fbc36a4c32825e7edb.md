# 12. Arrays

An array is a data structure that contains a number of variables which are accessed through computed indices. The variables contained in an array, also called the elements of the array, are all of the same type, and this type is called the element type of the array.

An array has a rank which determines the number of indices associated with each array element. The rank of an array is also referred to as the dimensions of the array. An array with a rank of one is called a single-dimensional array. An array with a rank greater than one is called a multi-dimensional array. Specific sized multi-dimensional arrays are often referred to as two-dimensional arrays, three-dimensional arrays, and so on.

Each dimension of an array has an associated length which is an integral number greater than or equal to zero. The dimension lengths are not part of the type of the array, but rather are established when an instance of the array type is created at run-time. The length of a dimension determines the valid range of indices for that dimension: For a dimension of length N, indices can range from 0 to N – 1 inclusive. The total number of elements in an array is the product of the lengths of each dimension in the array. If one or more of the dimensions of an array have a length of zero, the array is said to be empty.

The element type of an array can be any type, including an array type.

# 12.1 Array types

An array type is written as a non-array-type followed by one or more rank-specifiers:

```
array-type:
    non-array-type  rank-specifiers

non-array-type:
    type

rank-specifiers:
    rank-specifier
    rank-specifiers  rank-specifier

rank-specifier:
    [ dim-separators_opt ]

dim-separators:
    ,
    dim-separators ,
```

A non-array-type is any type that is not itself an array-type.

The rank of an array type is given by the leftmost rank-specifier in the array-type: A rank-specifier indicates that the array is an array with a rank of one plus the number of ',' tokens in the rank-specifier.

The element type of an array type is the type that results from deleting the leftmost rank-specifier:

+   - An array type of the form T[R] is an array with rank R and a non-array element type T.
+   - An array type of the form T[R][R1]…[Rn] is an array with rank R and an element type T[R1]…[Rn].

In effect, the rank-specifiers are read from left to right before the final non-array element type. The type int[,][,][,] is a single-dimensional array of three-dimensional arrays of two-dimensional arrays of int.