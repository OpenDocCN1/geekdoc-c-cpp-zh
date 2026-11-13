During initialization of an array, it is not compulsory to specify the size, and the square brackets may be left empty [ ] as

```
int A[]={3,4,5,2,8};
```

In this case, the compiler will assume the size of the array that matches the number of values in the braces { }.

# 4.5 ACCESSING VALUES OF AN ARRAY

The elements of an array can be accessed individually like normal variables, thus being able to read and modify their values. The format is as follows:

```
Array-name[index]
```

Consider the previous example in which A had 5 elements, and each of those elements was of type int the name that is used to refer each element is given in Figure 4.10.

| A[0] | A[1] | A[2] | A[3] | A[4] |
|---|---|---|---|---|
| | | | | |

# Figure 4.10 Referencing elements

To store the value 75 in the third element of A, the statement is written as A[2]=75; to pass the value of the third element of A to any variable then the statement is a = A[2]. Notice that the third element of A is specified as A[2], since the array index starts from zero, i.e. the first one is A[0], the second one is A[1], so the third one is A[2] and the last element is A[4]. Therefore, A[5] refers to the sixth element of A and this exceeds the size of the array.

In C++ it is syntactically correct to exceed the valid range of indices for an array. This will create problems, since accessing out-of-range elements do not cause compilation errors but can cause run-time errors. At this point it is important to clearly distinguish between the two uses of subscripts [ ] related to arrays. They perform two different tasks: one is to specify the size of arrays when they are declared, and the second one is to specify indices for concrete array elements.

```
int A[5];        //declaration of a new array
A[2];            //access to an element of the array
```

The data type always precedes a variable or array declaration, while it never precedes an access.

# 4.6 ARRAY OPERATIONS

Various operations that can be performed on array are

+   - Traversing
+   - Insertion
+   - Deletion
+   - Sorting
+   - Searching