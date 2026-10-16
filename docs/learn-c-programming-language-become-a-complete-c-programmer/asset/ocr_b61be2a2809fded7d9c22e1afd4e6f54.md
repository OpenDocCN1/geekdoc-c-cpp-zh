# A Matrix Design

> *Never express yourself more clearly than you are able to think.*  
> — Niels Bohr

# 29.1 Introduction

A language feature in isolation is boring and useless. This chapter demonstrates how features can be used in combination to address a challenging design task: a general N-dimensional matrix.

I have never seen a perfect matrix class. In fact, given the wide variety of uses of matrices, it is doubtful whether one could exist. Here, I present the programming and design techniques needed to write a simple N-dimensional dense matrix. If nothing else, this **Matrix** is far easier to use, and just as compact and fast, as anything a programmer would have time to write using **vectors** or builtin arrays directly. The design and programming techniques used for **Matrix** are widely applicable.

# 29.1.1 Basic Matrix Uses

**Matrix<T,N>** is an **N**-dimensional matrix of some value type **T**. It can be used like this:

```
```cpp
// zero dimensions: a scalar
// one dimension: a vector (4 elements) // twodimensions (4*3 elements)

Matrix<double,0> m0 {1};
Matrix<double,1> m1 {1,2,3,4}; Matrix<double,2> m2 {

{00,01,02,03}, // row0
{10,11,12,13}, // row1
{20,21,22,23}, // row2
};
Matrix<double,3> m3(4,7,9); // three dimensions (4*7*9 elements), all 0-initialized
Matrix<complex<double>,17> m17; // 17 dimensions (no elements so far)
```
```

The element type must be something we can store. We do not require every property that we have for a floating-point number from every element type. For example:

```
```cpp
Matrix<double,2> md; // OK
Matrix<string,2> ms; // OK: just don’t try arithmetic operations
Matrix<Matrix<int,2>,2> mm { // 3-by-2 matrix of 2-by-2 matrices
// a matrix is a plausible “number”

{// row0
{{1, 2}, {3, 4}}, // col 0
{{4, 5}, {6, 7}}, // col 1
```
```