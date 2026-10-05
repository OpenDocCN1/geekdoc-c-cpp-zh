```
/* Matrix cross product */
template<class T>
valarray<T> matult(
    const valarray<T>& a, size_t arows, size_t acols,
    const valarray<T>& b, size_t brows, size_t bcols) {
    /* Condition: acols =
    valarray<T> result(arows * bcols);
    for(size_t i = 0; i < arows; ++i)
        for(size_t j = 0; j < bcols; ++j) {
            auto row = a[slice(acols*i, acols, 1)]; // Row
            auto col = b[slice(j, brows, bcols)]; // Column
            result[i*bcols+j] = (row*col).sum(); // Cross product of rows
        }
    }
    return result;
}

int main() {
    constexpr int n = 3;
    valarray ma{1,0,-1, 2,2,-3, 3,4,0}; // 3 x 3 matrix
    valarray mb{3,4,-1, 1,-3,0, -1,1,2}; // 3 x 3 matrix
    printMatrix(cout, ma, n);
    cout << " -times-\n";
    printMatrix(cout, mb, n);
    cout << " -results in:-\n";
    valarray<int> mc = matult(ma, n, n, mb, n, n);
    printMatrix(cout, mc, n);
}
```

The output is {{4,3,-3}, {11,-1,-8}, {13,0,-3}} matrix, which represents the product of the matrix multiplication. Note that matult should only receive matrices and size specifications that are compatible for this operation.

With a[slice(...)] and b[slice(...)], a row or column is cleverly sliced out here. As the rule of matrix multiplication states, these are then multiplied element-wise and summed up: this is done with valarray in the innocuous-looking expression (row * col).sum().