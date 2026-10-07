524

THE MATRIX AND VECTOR CLASSES

The method definitions are then provided in the listing.

# Listing D.4 vector.cpp

```
//vector.cpp
#include <iostream>
#include <cstdlib>
#include <new>
#include "vector.h"

using std::cout; using std::endl;

Vector::Vector(int rows, double const* pa){
nRows = rows;
pA = new(std::nothrow) double[nRows];
pointerCheck();
}

for(int i = 0; i < nRows; i++)
pa[i] = pa[i];
}

Vector::Vector(int rows, double b){
nRows = rows;
if(nRows == 0) {
pA = 0;
return;
}
pA = new(std::nothrow) double[nRows];
pointerCheck();
}

for(int i = 0; i < nRows; i++)
pa[i] = b;
}

Vector::Vector(const Vector& v){
nRows = v.nRows;
pA = new(std::nothrow) double[nRows];
pointerCheck();
}

for(int i = 0; i < nRows; i++)
pa[i] = v.pa[i];
}

Vector::~Vector() {
delete [] pA;
}

double Vector::dotProd(const Vector& v) const {
double dot = 0;
for(int i = 0; i < nRows; i++)
dot += v.pa[i]*pa[i];
return dot;
}

Vector& Vector::operator=(const Vector& v) {
if(this == &v)//avoid self assignment
return *this;
}

//define/redefine object's members
if(nRows != v.nRows) {

if(pA != 0)
delete [] pA;

nRows = v.nRows;
pA = new(std::nothrow) double[nRows];
pointerCheck();
n}
```