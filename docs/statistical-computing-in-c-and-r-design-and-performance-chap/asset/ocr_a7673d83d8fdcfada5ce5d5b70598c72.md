# SOLVING LINEAR EQUATIONS

This class has the usual pointer-to-pointer and diagonal matrix (default) constructors, a
copy constructor, an explicit destructor to release the memory in the private member pA
 overloaded assignment and indexing operators. Accessors are provided to give
access to the private members nRows and nCols.

The principal difference between the Matrix class in Listing 7.7 and previous incarnations
how we handle the solution of linear equations. The gauss method has been wrapped in
a virtual function solve. The intention is to use a band-limited formulation for solve in
pBand class that will be derived from class Matrix.

The header file for the pdBand class is given in the following list:

# Listing 7.8 pdBand.h

```
//pdBand.h
#ifndef PDBAND_H
#define PDBAND_H
#include <iostream>
#include "simpleMatrix.h"
#include "vector.h"

class pdBand : public Matrix{
    int q& = bandwidth
    Vector bandBack(const Vector& RHS) const;
    Vector bandForward(const Vector& RHS) const;
    Vector bandchol(const Vector& RHS) const;

public:
    pdBand(int nRows, int q = -1, double a = 0.);
    pdBand(int nRows, int q, const pdBand* const* pa);
    pdBand(const pdBand& A);

    ~pdBand();

    Vector solve(const Vector& RHS) const {
        std::cout << "Solution via banded Cholesky from class PdBand"
                  << std::endl;
        return bandChol(RHS);
    }

    Matrix bandToFull() const;
};
#endif
```

The class declaration for pdBand begins on line 8 of Listing 7.8. It takes the usual format except
that has been augmented by : Matrix to indicate that pdBand is a derived class
that inherits the public members and member functions from its parent class Matrix. It
entails that a pdBand object can use getRows, getCols, the indexing operator, etc., using
an an object from class Matrix without having to include it in the class declaration.
Addition to the members that pdBand inherits from class Matrix it has its own
m q that will hold the bandwidth of the matrix. In this mind, it is highly
useful at this point to detail the plan for storing the matrix elements in a pdBand object.
If A is an n n symmetric banded matrix with bandwidth q and elements a_{ij},i,j =
1,...,n, it is only necessary to store its diagonal and above diagonals. This means