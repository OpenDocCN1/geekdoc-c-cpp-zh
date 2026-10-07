
# 514

# THE MATRIX AND VECTOR CLASSES

```cpp
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

```cpp
Matrix::operator+(const Matrix& B) const {
    if(nRows != B.nRows || nCols != B.nCols){
        cout << "Bad row and column dimensions in !" << endl;
        exit(1);
    }
    Matrix temp(nRows, nCols);
    for(int i = 0; i < nRows; i++)
        for(int j = 0; j < nCols; j++)
            temp.pA[i][j] = this->pA[i][j] + B.pA[i][j];
    return temp;
}
```

```cpp
Matrix::operator+=(const Matrix& B){
    if(nRows != B.nRows || nCols != B.nCols){
        cout << "Bad row and column dimensions in +=!" << endl;
        exit(1);
    }
    for(int i = 0; i < nRows; i++)
        for(int j = 0; j < nCols; j++)
            pA[i][j] += B.pA[i][j];

return *this;
}
```

```cpp
Matrix::operator-(const Matrix& B) const {
    if(nRows != B.nRows || nCols != B.nCols){
        cout << "Bad row and column dimensions in -!" << endl;
        exit(1);
    }
    Matrix temp(nRows, nCols);
    for(int i = 0; i < nRows; i++)
        for(int j = 0; j < nCols; j++)
            temp.pA[i][j] = this->pA[i][j] - B.pA[i][j];

return temp;
}
```

```cpp
Matrix::operator-=(const Matrix& B){
    if(nRows != B.nRows || nCols != B.nCols){
        cout << "Bad row and column dimensions in -=!" << endl;
        exit(1);
    }
    for(int i = 0; i < nRows; i++)
        for(int j = 0; j < nCols; j++)
            pA[i][j] -= B.pA[i][j];

return *this;
}
```

```cpp
Matrix::operator*(const Matrix& B) const {
    if(nRows != B.nRows || nCols != B.nCols){
        cout << "Bad row and column dimensions in *!" << endl;
        exit(1);
    }
    Matrix C(nRows, B.nCols); // matrix of all Os
    for(int i = 0; i < nRows; i++)
        for(int j = 0; j < B.nCols; j++)
            for(int k = 0; k < B.nRows; k++)
                C.p[i][j] += pA[i][k]*B.p[k][j];

return C;
}

Matrix::operator*(double b) const {
    Matrix C(nRows, nCols); // matrix of all Os
    for(int i = 0; i < nRows; i++)
        for(int j = 0; j < nCols; j++)
            C.p[i][j] = b*pA[i][j];

return C;
}

Matrix::operator*(const Vector& v) const {
    double temp;
    Vector C(nRows); // matrix of all Os
    for(int i = 0; i < nRows; i++) {
        temp = 0;
        for(int j = 0; j < nCols; j++)
            temp += pA[i][j]*v[j];
        C.p[i] = temp;
    }

return C;
}

// matrix operations
Matrix::trans() const {
    Matrix B(nCols, nRows, 0.0);
    for(int i = 0; i < nCols; i++)
        for(int j = 0; j < nRows; j++)
            B.p[i][j] = pA[j][i];
    return B;
}

// solution of a linear system
Vector::backward(const Vector& RHS) const {
    double temp; // temporary storage
    Vector b(nRows, 0.0);
    // initialize the recursion
    if(pA[nRows-1][nRows-1] != 0)
        b[nRows-1] = RHS[nRows-1]/pA[nRows-1][nRows-1];
    else {
        cout << "Singular system!" << endl;
        exit(1);
    }
    // now work through the remaining rows
    for(int i = nRows-2; i >= 0; i--) {
        if(pA[i][i] != 0) {
            temp = RHS[i];
            for(int k = i+1; k < nRows; k++)
                temp -= b[k]*pA[i][k];
            b[i] = temp/pA[i][i];
        } else {
            cout << "Singular system!" << endl;
            exit(1);
        }
    }
    return b;
}

Vector Matrix::forward(const Vector& RHS) const {
    double temp; // temporary storage
    Vector b(nRows, 0); // solution matrix
    // initialize the recursion
    if(pA[0][0] != 0)
        b[0] = RHS[0]/pA[0][0];
    else {
        cout << "Singular system!" << endl;
        exit(1);
    }
    // now work through the remaining rows
    for(int i=1; i<nRows; i++) {
        if(pA[i][i] != 0) {
            temp = RHS[i];
            for(int k = 0; k < i; k++)
                temp -= b[k]*pA[i][k];
            b[i] = temp/pA[i][i];
        } else {
            cout << "Singular system!" << endl;
            exit(1);
        }
    }
    return b;
}

Vector Matrix::gauss(const Vector& RHS) const {
    double multiplier = 0;
    Matrix G(nRows, nRows, pA);
    Vector h(nRows, RHS);

    for(int j=0; j < nCols; j++) { // column to be swept
        for(int jj = j; jj < nCols; jj++) { // current operation
            if(G[jj][j] == 0) {
                cout << "Oops! Division by zero!" << endl;
                exit(1);
            }
            for(int i = j+1; i < nRows; i++) { // do the same to the RHS
                multiplier = G[i][j]/G[jj][j];
                G[i][jj] -= multiplier*G[jj][jj];
                h[i] -= multiplier*h[j]; // Note: logic in OCR text seems slightly fragmented here
            }
        }
    }
    // now solve
    Vector b = G.backward(h);
    return b;
}

Vector Matrix::cholesky(const Vector& RHS) const {
    double temp = 0;
    Matrix G(nRows, nCols, 0);
    for(int j = 0; j < nCols; j++) { // proceed columns
        if(pA[j][j] == 0) { // This logic seems incomplete in the OCR
            // ... standard cholesky logic
        }
        temp = pA[j][j]; // starting value for diagonal element
        if (j > 0) {
            for(int k = 0; k < j; k++)
                temp -= G[j][k]*G[j][k];
        }
        G[j][j] = sqrt(temp);

        for(int i = j + 1; i < nRows; i++) { // do the rest
            temp = pA[j][i];
            for(int k = 0; k < j; k++)
                temp -= G[i][k]*G[j][k];
            G[i][j] = temp/G[j][j];
        }
    }

    cout << "Cholesky factor:" << endl;
    G.printMatrix();
    Vector h = G.forward(RHS);
    Vector b = G.trans().backward(h);
    return b;
}

Vector Matrix::backsub(const Vector& RHS, int bWidth) const {
    double temp; // temporary storage
    int up;
    Vector b(nRows, 0); // solution vector

    // initialize the recursion
    if(pA[nRows-1][nRows-1] != 0)
        b[nRows-1] = RHS[nRows-1]/pA[nRows-1][nRows-1];
    else {
        cout << "Singular system!" << endl;
        exit(1);
    }

    // work through the remaining rows
    for(int i = nRows - 2; i >= 0; i--) {
        if(pA[i][i] != 0) {
            temp = RHS[i];
            up = std::min(nCols, i + bWidth);
            for(int k = i + 1; k < up; k++)
                temp -= b[k]*pA[i][k];
            b[i] = temp/pA[i][i];
        } else {
            cout << "Singular system!" << endl;
            exit(1);
        }
    }
    return b;
}

Vector Matrix::bandFor(const Vector& RHS, int bWidth) const {
    double temp; // temporary storage
    int low;
    Vector b(nRows, 0); // solution vector

    // initialize the recursion
    if(pA[0][0] != 0)
        b[0] = RHS[0]/pA[0][0];
    else {
        cout << "Singular system!" << endl;
        exit(1);
    }
    // ... rest of band implementation
    return b;
}
