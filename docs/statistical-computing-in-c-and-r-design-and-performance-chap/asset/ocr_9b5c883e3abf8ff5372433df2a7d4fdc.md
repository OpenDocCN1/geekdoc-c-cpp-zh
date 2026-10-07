# 84 A SKETCH OF C++

```
}
Matrix* m2 = new Matrix(3, 2, p);
cout << "Here is a matrix initialized by a pointer-to-pointer" << endl;
m2->printMatrix();
return 0;
}
```

This program creates an identity format and another matrix with nonzero off-diagonal elements using the pointer-to-pointer storage. Both a Matrix object and a pointer to a Matrix object are used to represent the matrices using the syntax that is used in the two cases.

An associated myfile for our Matrix class code might look like

```
simpleMat : simpleDriver.o simpleMatrix.o
 g++ -Wall simpleDriver.o simpleMatrix.o -o simpleMat
```

```
simpleMatrix.o : simpleMatrix.cpp simpleMatrix.h
 g++ -c -Wall simpleMatrix.cpp
```

```
simpleDriver.o : simpleDriver.cpp simpleMatrix.h
 g++ -c -Wall simpleDriver.cpp
```

The output from execution of our code is then to be

Here is an identity matrix

+   1 0
0 1

Here is a matrix initialized by a pointer-to-pointer

+   1 2
2 4
3 6

Our class has limited utility in that to create an object from the class. The next step is to expand on this skeleton structure to create functionality including the provision of methods for matrix addition, multiplication, etc. It is possible to accomplish this through operator overloading as will eventually be demonstrated. But, it is first to deal with the concept of a copy constructor for our class.

We eventually want to use matrix objects as arguments to functions or in assignments (via =). In particular, this means that there will be occasions when a copy of a matrix object is created. This is accomplished using the default copy constructor that is implied by C++ for every class unless an explicit copy constructor is defined. The implicit copy constructor makes an element-by-element copy of the members of the class and this is not always desirable.

An illustration of how the default copy constructor will behave for our class Matrix can be obtained by attempting to run

```
//copyEx.cpp
#include "simpleMatrix.h"
#include <iostream>
```

```
using std::cout; using std::endl;
void g(Matrix A){};
```

```
int main(){
Matrix m(2, 2, 1.);
```