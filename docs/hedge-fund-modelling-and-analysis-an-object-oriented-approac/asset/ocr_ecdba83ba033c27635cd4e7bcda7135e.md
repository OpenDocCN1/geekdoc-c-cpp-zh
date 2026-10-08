```
Matrix res = a;
res.Add(b);
return res;

// Subtract a Matrix from a Matrix (-)
Matrix operator-(const Matrix& a, const Matrix& b)
{
// Check if dimensions match
if (a.rows == b.rows && a.cols == b.cols)
{
    Matrix res(a.rows, a.cols);

    for (UINT r=0; r<a.rows; r++)
    {
        for (UINT c=0; c<a.cols; c++)
        {
            res.p[r][c] = a.p[r][c] - b.p[r][c];
        }
    }
    return res;
}else
{
    cout << "\nDimensions does not match\n";
}
// Return empty matrix
return Matrix();
}

// Subtract Matrix by double (-)
Matrix operator-(const Matrix& a, const DBL b)
{
    Matrix res = a;
res.Subtract(b);
    return res;
}

// Subtract double by Matrix (-)
Matrix operator-(const DBL b, const Matrix& a)
{
    Matrix res = -a;
res.Add(b);
    return res;
}
```