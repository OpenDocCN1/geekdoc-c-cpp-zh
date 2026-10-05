# 3.2. Compiler optimizations

C++ function timed in table 3.4 uses Matrix class objects (see chapter 1 for the definition of the Vector class, the Matrix class is similar).¹7

If matrices are multiplied using objects of the class Matrix, the C++ syntax mimics mathematical syntax quite closely as shown below.

```
void multijk(Matrix& A, Matrix& B, Matrix& C){
  int l = A.getm();
  int m = A.getn();
  assrt(B.getm()==m);
  int n = B.getn();
  assrt(C.getn()==1);
  assrt(C.getn()==n);
  for(int i=0; i < l; i++)
    for(int j=0; j < m; j++)
      for(int k=0; k < n; k++)
        C(i,k) += A(i,j)*B(j,k);
```

The price paid for staying close to mathematical syntax is very performance. Comparing tables 3.3 and 3.4, we find that on AVX2, the C++ is slower than MKL BLAS by a whopping factor that is nearly 100!

The multiplication program here may look nice to a human reader. But a usage such as C(i,j) is in fact an overloaded function call. It is much difficult for the compiler to figure out the pattern in which the indices are mapping to locations in the array. If we want the compiler to do a good job, we have to make the loops easy and optimize for the compiler.

Of course, the fault is not that of C++. C++ provides a gigantic vocabulary and numerous modes of expression. It is for the programmer to decide how to use it.

To this end, we turn to the persistent belief in some quarters that Fortran programs are faster than C or C++ programs. The basis of this belief is that arrays do not alias in Fortran the way pointers can alias in C/C++. As we have seen in this chapter, the assurance of no aliasing allows the compiler to generate better code. Given that the restrict qualifier was introduced only around 2000 and was

¹⁷The timing information was collected with function inlining enabled.