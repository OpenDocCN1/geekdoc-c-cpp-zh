# 17. Arrays

# 17.1 General

An array is a data structure that contains a number of variables that are accessed through computed indices. The variables contained in an array, also called the elements of the array, are all of the same type, and this type is called the element type of the array.

An array has a rank that determines the number of indices associated with each array element. The rank of an array is also referred to as the dimensions of the array. An array with a rank of one is called a single-dimensional array. An array with a rank greater than one is called a multi-dimensional array. Specific sized multi-dimensional arrays are often referred to as two-dimensional arrays, three-dimensional arrays, and so on. Each dimension of an array has an associated length that is an integral number greater than or equal to zero. The dimension lengths are not part of the type of the array, but rather are established when an instance of the array type is created at run-time. The length of a dimension determines the valid range of indices for that dimension: For a dimension of length N, indices can range from 0 to N − 1 inclusive. The total number of elements in an array is the product of the lengths of each dimension in the array. If one or more of the dimensions of an array have a length of zero, the array is said to be empty.

Every array type is a reference type (§9.2). The element type of an array can be any type, including value types and array types.

# 17.2 Array types

# 17.2.1 General

The grammar productions for array types are provided in §9.2.1.

An array type is written as a non-array-type followed by one or more rank-specifiers.

A non-array-type is any type that is not itself an array-type.

The rank of an array type is given by the leftmost rank-specifier in the array-type: A rank-specifier indicates that the array is an array with a rank of one plus the number of ',' tokens in the rank-specifier.

The element type of an array type is the type that results from deleting the leftmost rank-specifier:

+   - An array type of the form T[R] is an array with rank R and a non-array element type T.
+   - An array type of the form T[R][R1]...[Rr] is an array with rank R and an element type T[R1]...[Rr].

In effect, the rank-specifiers are read from left to right before the final non-array element type. [Example: The type int[][ , ][ , ] is a single-dimensional array of three-dimensional arrays of two-dimensional arrays of int. end example]

At run-time, a value of an array type can be null or a reference to an instance of that array type. [Note: Following the rules of §17.6, the value may also be a reference to a covariant array type. end note]

# 17.2.2 The System.Array type

The type System.Array is the abstract base type of all array types. An implicit reference conversion (§11.2.7) exists from any array type to System.Array and to any interface type implemented by System.Array. An explicit reference conversion (§11.3.5) exists from System.Array and any interface type implemented by System.Array to any array type. System.Array is not itself an array-type. Rather, it is a class-type from which all array-types are derived.

At run-time, a value of type System.Array can be null or a reference to an instance of any array type.