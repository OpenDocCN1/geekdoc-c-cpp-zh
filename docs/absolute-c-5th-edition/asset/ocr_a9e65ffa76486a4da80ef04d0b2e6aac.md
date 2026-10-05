# CHAPTER 14 Inheritance

# EXAMPLE: (continued)

Consider the member function backup. In our previous implementation (Display 14.11), we copied the array entries from a to b. Since a is now private, we cannot access it by name, but we have overloaded the array square bracket operator operator[] so that it applies to type PFArray, and this operator is inherited in PFArrayDBak. We simply use operator[] with the calling object. The net effect is to copy from the array to the array b, but we prevent the private array by a name. The code for this is:

```
usedB = getUsed();
for (int i = 0; i < usedB; i++)
 b[i] = operator[](i);
```

Be sure to note the syntax for calling an operator of the class being. If superArray is an object of the class PFArrayDBak, then in the invocation superArray.backup(), the notation operator[] means superArray[i].
We could have used the notation operator[](i) in our definition of the member function restore, but it is just to empty the array with the inherited member function emptyArray and then add the backed-up elements using createElement. This way, we also set the private member variable used in the process.
With this alternate implementation, the class PFArrayDBak is used just as it was with the previous implementation. In particular, the demonstration program in Display 14.12 works exactly the same for each implementation.

14.13 Alternate Implementation of PFArrayDBak (part 1 of 2)

```
1 //This is the file pfarraydbak.cpp.
2 //This is the implementation of the class PFArrayDBak.
3 //The interface for the class PFArrayDBak is in the file pfarraydbak.h.
4 #include "pfarraydbak.h"
5 #include <iostream>
6 using std::cout;

7 PFArrayDBak::PFArrayDBak() : PFArrayD(), usedB(0)
8 {
9 b = new double[getCapacity()];
10 }
11 PFArrayDBak::PFArrayDBak(int capacityValue) : PFArrayD(capacityValue)
      usedB(0)
12 {
13 b = new double[getCapacity()];
14 }
```