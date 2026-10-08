
```cpp
for (UINT c=1; c<=cols - (col >= cols); c++)
{
    res(r - (r > row), c - (c > col)) = p[r-1][c-1];
}
}
else
{
    cout << "*\n Index for minor out of range\n";
}

return res;
```

```cpp
// Matrix diagonal
Matrix Matrix::Diag(const int n)
{
    Matrix res = Matrix(n,n);

    for (int i = 1; i <= n; i++)
    {
        res(i, i) = 1;
    }
    return res;
}
```

```cpp
// Matrix diagonal
Matrix Matrix::Diag(const Matrix& v)
{
    Matrix res;

    if (v.GetCols() == 1)
    {
        // the given matrix is a vector n x 1
        int rows = v.GetRows();
        res = Matrix(rows
```

```cpp
// Matrix is a vector 1 x n
int cols = v.GetCols();
res = Matrix(cols, cols);

// Copy values of vector to Matrix
for (int c=1; c <= cols; c++)
{
    res(c, c) = v.Get(1, c);
}
else
{
    cout << "\n Parameter for diagonal must be a vector\n";
    return res;
}

// Matrix determinant
DBL Matrix::Det(const Matrix& a)
{
    DBL d = 0; // Value of the determinant
    int rows = a.GetRows();
    int cols = a.GetRows();

    if (rows == cols)
    {
        // A square matrix
        if (rows == 1)
        {
            // A 1 x 1 matrix
            d = a.Get(1, 1);
        }
        else if (rows == 2)
        {
            // A 2 x 2 matrix
            // Determinant of [a11,a12;a21,a22] is det = a11*a22-a21*a12
            d = a.Get(1, 1) * a.Get(2, 2) - a.Get(2, 1) * a.Get(1, 2);
        }
        else
        {
            // A 3 x 3 matrix or larger
            for (int c = 1; c <= cols; c++)
            {
                Matrix M = a.Minor(1, c);
                //d += pow(-1, 1+c) * a(1, c) * Det(M);
                d += (c2 & c-1) * a.Get(1, c) * Det(M); // Faster than pow
            }
        }
    }
}
else
{
    cout << "\n Matrix must be square!\n*";
    return d;
}

// Matrix inverse
Matrix Matrix::Inv(const Matrix& a)
{
    Matrix res;
    double d = 0; // Value of the determinant
    int rows = a.GetRows();
    int cols = a.GetCols();

    d = Det(a);
    if (rows == cols && d != 0)
    {
        // A square matrix
        if (rows == 1)
        {
            // A 1 x 1 matrix
            res = Matrix(rows, cols);
            res(1, 1) = 1 / a.Get(1, 1);
        }
        else if (rows == 2)
        {
            // A 2 x 2 matrix
            res = Matrix(rows, cols);
            res(1, 1) = a.Get(2, 2);
            res(1, 2) = -a.Get(1, 2);
            res(2, 1) = -a.Get(2, 1);
            res(2, 2) = a.Get(1, 1);
            res = (1/d) * res;
        }
        else
        {
            // A matrix of 3 x 3 or larger
            // Calculate inverse using Gauss-Jordan elimination
            res = Di(rows); // A diagonal Matrix
            Matrix ai = a; // Make a copy of Matrix a
        }
    }

    for (int c = 1; c <= cols; c++)
```

```cpp
// Element (c, c) should be non-zero.
// If not, swap content of lower rows
int r;
for(r=c; r<=rows && ai(r, c) == 0; r++)
{
    if (r != c)
    {
        // Swap rows
        for (UINT s=1; s<=cols; s++)
        {
            Swap(ai(c, s), ai(r, s));
            Swap(res(c, s), res(r, s));
        }
    }

    // Eliminate non-zero values on the other rows at column c
    for (UINT r=1; r<=rows; r++)
    {
        if (r != c)
        {
            // eliminate value at column c and row r
            if (ai(r, c) != 0)
                double f = - ai(r, c) / ai(c, c);

            // Add (f * row c) to row r to eliminate the value at column c
            for (UINT s=1; s<=cols; s++)
            {
                ai(r, s) += f * ai(c, s);
                res(r, s) += f * res(c, s);
            }
        }
    }
}
else
{
    // Make value at (c, c) one,
    // Divide each value on row r with the value at ai(c, c)
    double f = ai(c, c);
    for (UINT s=1; s<=cols; s++)
    {
        ai(r, s) /= f;
        res(r, s) /= f;
    }
}
}
else {
    if (rows == cols) {
        cout << "\n Matrix must be square!\n";
    }
    else {
        cout << "\n Determinant of matrix is zero\n";
    }
}

return res;
}

// # rows
int Matrix::GetRows() const {
    return rows;
}

// # columns
int Matrix::GetCols() const {
    return cols;
}

// Get index
DBL Matrix::GetConst(const int r, const int c) const {
    if (p != NULL && r > 0 && r <= rows && c > 0 && c <= cols) {
        return p[r-1][c-1];
    }
    else {
        cout << "\n Subscript out of range\n";
    }
}
```

Source 6.5 shows the implementation of the method of Lagrange multipliers to find the optimised set of weights for a target portfolio return of 9.0% in our 10-hedge-fund portfolio.

# SOURCE 6.5: IMPLEMENTATION OF THE METHOD OF Lagrange Multipliers

```cpp
// ...
// Optimise.h
//...

Matrix MLM(const V2DD& v, const DBL rtar); // MLM

//...
```

```cpp
Matrix Optimise::MLM(const V2DD& v, const DBL rtar)
{
    UINT n = v[0].size(-1);

    Matrix o = Matrix(n, 1);    // Matrix of ones
    Matrix oT = Matrix(1, n);   // Ones transposed
    Matrix R = Matrix(n, 1);    // R Matrix
    Matrix RT = Matrix(1, n);   // R transposed
    Matrix V = Matrix(n, n);    // VCV Matrix
    Matrix Vi = Matrix(n, n);  // VCV inverse

    // o Matrix
    for (UINT i=1; i<=n; i++)
        o(i, 1) = 1.0;

    // transpose
    for (UINT i=1; i<=n; i++)
        oT(i, 1) = 1.0;

    // Mean returns
    V1DD r = Mean(v, 12);

    // R matrix
    for (UINT i=1; i<=n; i++)
        R(i, 1) = r[i-1];

    // R transpose
    for (UINT i=1; i<=n; i++)
        RT(i, 1) = 1.0;
```

```cpp
// Covariance matrix
Matrix V = Matrix(n, n);    // VCV Matrix
Matrix Vi = Matrix(n, n);  // VCV inverse

// o Matrix
for (UINT i=1; i<=n; i++)
    o(i, 1) = 1.0;

// transpose
for (UINT i=1; i<=n; i++)
    oT(i, 1) = 1.0;

// Mean returns
V1DD r = Mean(v, 12);

// R matrix
for (UINT i=1; i<=n; i++)
    R(i, 1) = r[i-1];

// R transpose
for (UINT i=1; i<=n; i++)
    RT(i, 1) = 1.0;
```
