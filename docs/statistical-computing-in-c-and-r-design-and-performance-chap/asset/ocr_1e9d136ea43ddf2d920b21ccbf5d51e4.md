# 514

# THE MATRIX AND VECTOR CLASSES

```
pointerCheck();

for(int i = 0; i < nRows; i++){
    pA[i] = new(std::nothrow) double[nCols];
    pointerCheck(i);
}
for(int i = 0; i < nRows; i++)
    for(int j = 0; j < nCols; j++)
        pA[i][j] = A.pA[i][j];

return *this;
```

```
Matrix::operator+(const Matrix& B) const {
    if(nRows != B.nRows || nCols != B.nCols){
        cout << "Bad row and/ column dimensions in !" << endl;
        exit(1);
    }
    Matrix temp(nRows, nCols);
    for(int i = 0; i < nRows; i++)
        for(int j = 0; j < nCols; j++)
            temp.pA[i][j] = this->pA[i][j] + B.pA[i][j];
    return temp;
```

```
Matrix::operator+=(const Matrix& B){
    if(nRows != B.nRows || nCols != B.nCols){
        cout << "Bad row and/ column dimensions in ++!" << endl;
        exit(1);
    }
    for(int i = 0; i < nRows; i++)
        for(int j = 0; j < nCols; j++)
            pA[i][j] += B.pA[i][j];

return *this;
```

```
Matrix::operator-(const Matrix& B) const {
    if(nRows != B.nRows || nCols != B.nCols){
        cout << "Bad row and/ column dimensions in -!" << endl;
        exit(1);
    }
    Matrix temp(nRows, nCols);
    for(int i = 0; i < nRows; i++)
        for(int j = 0; j < nCols; j++)
            temp.pA[i][j] = this->pA[i][j] - B.pA[i][j];

return temp;
```

```
Matrix::operator-=(const Matrix& B){
    if(nRows != B.nRows || nCols != B.nCols){
        cout << "Bad row and/ column dimensions in -=!" << endl;
        exit(1);
    }
    for(int i = 0; i < nRows; i++)
        for(int j = 0; j < nCols; j++)
            pA[i][j] -= B.pA[i][j];

return *this;
```

```
Matrix::operator*(const Matrix& B) const {
    if(nRows != B.nRows || nCols != B.nCols){
        cout << "Bad row and column dimensions in *!" << endl;
        exit(1);
    }
```