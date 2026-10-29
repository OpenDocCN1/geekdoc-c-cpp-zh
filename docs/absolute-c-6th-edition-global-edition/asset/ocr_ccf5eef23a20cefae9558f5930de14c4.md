# Display 16.8 Interface for the Template Class PFArrayBak

```
1 //This is the header file pfarraybak.h. This is the interface for the
2 //template class PFArrayBak. Objects of this type are partially filled
3 //arrays of any type T. This version allows the programmer to make a
4 //backup copy and restore to the last saved copy of the partially filled
//array.
5 #ifndef PFARRAYBAK_H
6 #define PFARRAYBAK_H
7 #include "pfarray.h"
8 
9 namespace PFArraySavitch
10 {
11     template<class T>
12     class PFArrayBak : public PFArray<T>
13     {
14     public:
15         PFArrayBak();
16         //Initializes with a capacity of 50.
17         PFArrayBak(int capacityValue);
18         PFArrayBak(const PFArrayBak<T>& object);
19         void backup();
20         //Makes a backup copy of the partially filled array.
21         void restore();
22         //Restores the partially filled array to the last saved version.
23         //If backup has never been invoked, this empties the partially
24         //filled array.
25         PFArrayBak<T>& operator =(const PFArrayBak<T>& rightSide);
26         virtual ~PFArrayBak();
27     private:
28         T *b; //for a backup of main array.
29         int usedB; //backup for inherited member variable used.
30     };
31 
32 } // PFArraySavitch
33 #endif //PFARRAY_H
```

# Display 16.9 Implementation for the Template Class PFArrayBak (part 1 of 3)

```
1 //This is the file pfarraybak.cpp.
2 //This is the implementation for the template class PFArrayBak. The
3 //interface for the template class PFArrayBak is in the file
4 //pfarraybak.h.
5 #include "pfarraybak.h"
6 #include <iostream>
```