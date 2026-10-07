# THE MATRIX AND VECTOR CLASSES

521

```
{
  bw = bw;
}

pdBand::pdBand(const pdBand& A)
{
  Matrix(A)
  bw = A.bw;
}

pdBand& pdBand::operator=(const pdBand& A){
  if(this == &A)//avoid self assignment
    return *this;
  this->Matrix::operator=(A);
  bw = A.bw;
  return *this;
}

Matrix pdBand::operator+(const Matrix& B) const {
  Matrix A = this->bandToFull();
  return (A + B);
}

pdBand& pdBand::operator=(const pdBand& B) const {
  pdBand temp(getRows(), B.bw);
  temp.Matrix::operator=(this->Matrix::operator+(B));
  return temp;
}

pdBand& pdBand::backward(const Vector& RHS) const {
  double temp;//temporary storage
  int up;
  int rows = this->getRows();
  Vector b(rows, 0.9);//solution vector
//initialize the recursion
if(pA[rows-1][0] != 0) {
  b.pA[rows-1] = RHS.pA[rows-1]/pA[rows-1][0];
} else {
  cout << "Singular system!" << endl;
  exit(1);
}
//now work through the remaining rows
for(int i=pA[i][0] != 0; i>=0; i--) {
  temp = std::min(rows, bw + 1);
  for(int k=i; k<up; k++) {
    temp -= b.pA[i+k]*pA[i][k];
  }
  b.pA[i] = temp/pA[i][0];
} else {
  cout << "Singular system!" << endl;
  exit(1);
}
return b;
}

pdBand pdBand::forward(const Vector& RHS) const {
  double temp;//temporary storage
  int low;
  int rows = this->getRows();
  Vector b(rows, 0.9);//solution vector
```