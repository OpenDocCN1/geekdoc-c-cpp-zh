# 644 CHAPTER 14 Inheritance

Display 14.11 Implementation for the Derived Class PFArrayDBak (part 2 of 2)

```
31 void PFArrayDBak::restore ( )
32 {
33     usedB = usedB;
34     for (int i = 0; i < usedB; i++)
35         a[i] = b[i];
36 }
```

```
37 PFArrayDBak& PFArrayDBak::operator = (const PFArrayDBak& rightSide)
38 {
39     int oldCapacity = capacity;
40     PFArrayD::operator = (rightSide);
41     if (oldCapacity != rightSide.capacity)
42     {
43         delete [] b;
44         b = new double[rightSide.capacity];
45     }
```

> Use the base class assignment operator in order to assign to the base class member variables.

```
46     usedB = rightSide.usedB;
47     for (int i = 0; i < usedB; i++)
48     b[i] = rightSide.b[i];
```

```
49     return *this;
50 }
```

```
51 PFArrayDBak()::~PFArrayDBak()
52 {
53     delete [] b;
54 }
```

> The destructor for the base class PFArrayD is called automatically, and it performs delete [] a;

Display 14.12 Demonstration Program for the PFArrayDBak (part 1 of 3)

```
1 //Program to demonstrate the class PFArrayDBak.
2 #include <iostream>
3 #include "pfarraydbak.h"
4 using std::cin;
5 using std::cout;
6 using std::endl;
```

```
7 void testPFArrayDBak() ( )
8 //Conducts one test of the class PFArrayDBak.
```

```
9 int main ()
10 {
11 cout << "This program tests the class PFArrayDBak.\n"; }
```