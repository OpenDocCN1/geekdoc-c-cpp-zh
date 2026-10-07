# 82 A SKETCH OF C++

using std::cout; using std::endl;

```
Matrix::Matrix(int nrows, int ncols, double a){
    nRows = nrows;
    nCols = ncols;
    //set pa to null pointer in default case
    if(nRows == 0 || nCols == 0) {
        pA = 0;
        return;
    }
    pA = new(std::nothrow) double*[nRows];
    pointerCheck();

for(int i = 0; i < nRows; i++){
    pA[i] = new(std::nothrow) double[nCols];
    pointerCheck(i);
    for(int j = 0; j < nCols; j++) {
        if(i == j)
            pA[i][j] = a;
        else
            pA[i][j] = 0;
    }
}
}
```

```
Matrix::Matrix(int nrows, int ncols, const double* const* pa){
    nRows = nrows;
    nCols = ncols;
    pA = new(std::nothrow) double*[nRows];
    pointerCheck();

for(int i = 0; i < nRows; i++){
    pA[i] = new(std::nothrow) double[nCols];
    pointerCheck(i);
}
}
```

```
for(int i = 0; i < nRows; i++) {
    for(int j = 0; j < nCols; j++) {
        pA[i][j] = pa[i][j];
    }
}
```

```
Matrix::~Matrix(){
if(pA != 0) {
    for(int i = 0; i < nRows; i++) {
        delete[] pA[i];
    }
    delete[] pA;
}
}
```

```
void Matrix::printMatrix() const {
for(int i = 0; i < nRows; i++) {
    for(int j = 0; j < nCols; j++) {
        cout << " " " << pA[i][j] << " ";
    }
    cout << endl;
}
}
```