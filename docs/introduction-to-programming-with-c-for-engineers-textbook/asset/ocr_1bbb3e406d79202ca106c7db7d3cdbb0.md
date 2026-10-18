the final result, which goes in the output matrix at the row-column position. For instance, multiplying the first row by the first column goes like this: 1 · 0 + 0 · 2.2 + (−5) · 3 = −15.

Armed with this knowledge, we are ready to write the code in Listing 3.23. The function `MultMatrix` for matrix multiplication is defined on line [20]. Again, it expects two `EMatrix` objects representing real matrices, passed by constant references a and b. But unlike matrix addition, matrix multiplication requires the number of columns of a be the same as the number of rows of b. After reading the numbers of rows and columns on lines [22–26], this condition is checked with `assert`. Then, on line [30], the return matrix c is created with values explicitly initialized to 0.0 (if not provided, 0 is used anyway).

```
**Listing 3.23** Definition of the matrix multiplication function (part of *EMUtility.cpp*).

```cpp
// Multiply two matrices, return the result:
// c = a * b
// Dimensions of a and b must comply for multiplication
EMatrix      MultMatrix( const EMatrix & a, const EMatrix & b )
{
    const auto a_cols = a.GetCols();
    const auto a_rows = a.GetRows();

    const auto b_cols = b.GetCols();
    const auto b_rows = b.GetRows();

    assert( a_cols == b_rows );          // Dimensions must be the same

    EMatrix c( a_rows, b_cols, 0.0 );    // Output matrix has such dimensions

    for( Dim ar = 0; ar < a_rows; ++ ar )       // Traverse rows of a
        for( Dim bc = 0; bc < b_cols; ++ bc )   // Traverse cols of b
            for( Dim ac = 0; ac < a_cols; ++ ac ) // Traverse cols of a == rows of b
                c.fData[ ar ][ bc ] += a.fData[ ar ][ ac ] * b.fData[ ac ][ bc ];

    return c;
}
```
```

From the previous example, we discover that matrix multiplication requires three loops: the first iterates through the rows of a, the second through the columns of b, and the third through the columns of a (which must number the same as the rows of b). These three loops are realized on lines [32–34] with `for` statements. Consecutive sums of products of corresponding elements of a and b are added on line [35] to the corresponding position of matrix c.

Finally, the resulting matrix c is returned on line [37]. Note at this point that c is returned by value, which can involve expensive object copying. This should not be a major problem thanks to the optimization mechanisms discussed in Section 4.6.4.

# 3.15.5  Organizing the Project Files and Running the Application

The previous code fragments come from the *EasyMatrix* project available from the book’s project web page (Cyanek 2018). The definition of the `EMatrix` structure is placed in the *EMatrix.h* header. Matrix operations are located in the *EMUtility.h* and *EMUtility.cpp* files, and test functions are in