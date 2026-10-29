# Display 14.9 Implementation for the Base Class PFArrayD (part 2 of 2)

```
29 PFArrayD& PFArrayD::operator = (const PFArrayD& rightSide)
30 {
31     if (capacity != rightSide.capacity)
32     {
33         delete [] a;
34         a = new double[rightSide.capacity];
35     }
36
37     capacity = rightSide.capacity;
38     used = rightSide.used;
39     for (int i = 0; i < used; i++)
40         a[i] = rightSide.a[i];
41     return *this;
42 }
43 PFArrayD::~PFArrayD()
44 {
45     delete [] a;
46 }
```

# Display 14.10 Interface for the Derived Class PFArrayDBak (part 1 of 2)

```
1 //This is the header file pfarraydbak.h. This is the interface for the
2 //class PFArrayDBak. Objects of this type are partially filled arrays
3 //of doubles.
4 //This version allows the programmer to make a backup copy and restore
5 //to the last saved copy of the partially filled array.
6 #ifndef PFARRAYDBAK_H
7 #define PFARRAYDBAK_H
8 #include "pfarrayd.h"
9
10 class PFArrayDBak : public PFArrayD
11 {
12 public:
13     PFArrayDBak();
14     //Initializes with a capacity of 50.
15
16     PFArrayDBak(int capacityValue);
17
18     PFArrayDBak(const PFArrayDBak& Object);
19
20     void backup();
21     //Makes a backup copy of the partially filled array.
22
23     void restore();
24     //Restores the partially filled array to the last saved version.
```