# MATRIX AND VECTOR CLASSES

in the header file and not in the method definition. We have done this for the diagonal matrix constructor in class Matrix with all three arguments given default values of 0. This has the consequence that the diagonal matrix constructor will serve as the default constructor because it can respond to nonspecific request for a Matrix object such as

```
Matrix A;
```

As be seen below, in this case the action of the constructor will be to return a Matrix object A with A.nCols = 0 and A.pa the nullptr.
The new feature in this Matrix class is the specification of two private, overloaded functions named pointercheck. These are simple functions that will check that memory allocations for the class pA and its associated matrix row points are successful. They are intended for internal use within the class and would be of no direct interest for users. It therefore means to designate them as private, and will (and not) modify class data members, and, have been designated as const member functions.

The next function is the destructor ~Matrix() and we need to discuss this concept before proceeding. All classes have a destructor acquired every time a class object goes out of scope. Thus, for example, our Power class has a default destructor supplied by the class. The compiler's destructor simply releases the memory for each of the classes (e.g., for the integer power K in the Power class) whenever a Power object goes out of scope. While this works for Power objects, for objects with dynamically allocated memory acquired with the new operator this is problematic. As a case in point, for an object of class Matrix a supplied destructor would release the memory that have been allocated to the pA. To avoid this when it happens pA points to memory locations that hold the values of pointers, which turn, hold the addresses for blocks of memory that have been allocated to the row elements of a two-dimensional array. Deleting pa releases this latter memory and has the side effect of making impossible to access any of the memory that was previously accessible by dereferencing pA. To avoid this type of memory leak it is necessary to provide an explicit destructor for the Matrix class that memory correctly in Section 3.5. This will be done in Listing 3.14 that provides the method definitions for the Matrix class. The general rule concerning destructors is that an explicit destructor should be supplied for any class that uses dynamic memory allocation.

The remainder of the Matrix header file gives the accessor functions getRows, getCols and the prototype for a print utility method printMatrix. The purpose of accessor functions is to provide nonnegative access to private members. The definitions for getRows and getCols are given inside the header file, as noted in Section 3.7, has the effect of making them inline functions. Functions of this nature tend to be only one or two of which make them suitable for inline treatment and we will generally use this option for the accessor functions that are encountered throughout the text. The accessors and the print utility should not alter a Matrix object and have accordingly designated as const member functions.

The next step is to create the definitions for the functions that are not defined in the header. These are given in Listing 3.14 below.

Listing 3.14 simpleMatrix.cpp

```
//simpleMatrix.cpp
#include <iostream>
#include <cstdlib>
#include <new>
#include "simpleMatrix.h"
```