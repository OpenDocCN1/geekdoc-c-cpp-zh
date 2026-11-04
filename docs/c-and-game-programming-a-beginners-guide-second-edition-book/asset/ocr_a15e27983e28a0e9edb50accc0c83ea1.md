```
Console.WriteLine();
}
}
```

> Note
> C# includes a localized reference when dealing with variables declared as part of the for loop. Thus any secondary for loops using the same variable name would also have to be redeclared. This differs from C++, which only asks for a second declaration if the variable falls out of scope.

You also should have noticed that our first array didn't have any individual values, i.e., the elements of the first dimension were actually only the first element of each of the secondary arrays. This is usually described as an array of arrays, but that tends to confuse people. The best way to think about it is as a set of single arrays listed together in a single column as demonstrated in Example 4.13.

a[0][0] a[0][1] A[0][2] a[0][3] a[0][4]
a[1][0] a[1][1] A[1][2] a[1][3] a[1][4]
a[2][0] a[2][1] A[2][2] a[2][3] a[2][4]
a[3][0] a[3][1] A[3][2] a[3][3] a[3][4]
a[4][0] a[4][1] A[4][2] a[4][3] a[4][4]
a[5][0] a[5][1] A[5][2] a[5][3] a[5][4]
a[6][0] a[6][1] A[6][2] a[6][3] a[6][4]
a[7][0] a[7][1] A[7][2] a[7][3] a[7][4]
a[8][0] a[8][1] A[8][2] a[8][3] a[8][4]
a[9][0] a[9][1] A[9][2] a[9][3] a[9][4]

Where, a[10][0]–a[10][4] are Null (\0).

# Example 4.13. Array values.