# Display 16.8 Interface for the Template Class PFArrayBak (part 2 of 2)

```
10  template<class T>
11  class PFArrayBak : public PFArray<T>
12  {
13  public:
14      PFArrayBak();
15      //Initializes with a capacity of 50.
16
17      PFArrayBak(int capacityValue);
18
19      PFArrayBak(const PFArrayBak<T>& Object);
20
21      void backup();
22      //Makes a backup copy of the partially filled array.
23
24      void restore();
25      //Restores the partially filled array to the last saved version.
26      //If backup has never been invoked, this empties the partially
27      //filled array.
28
29      PFArrayBak<T>& operator =(const PFArrayBak<T>& rightSide);
30
31      virtual ~PFArrayBak();
32  private:
33      T *b; //for a backup of main array.
34      int usedB; //backup for inherited member variable used.
35  };
36  }// PFArraySavitch
37  #endif //PFARRAY_H
```

# Display 16.9 Implementation for the Template Class PFArrayBak (part 1 of 3)

```
1  //This is the file pfarraybak.cpp.
2  //This is the implementation for the template class PFArrayBak. The
3  //interface for the template class PFArrayBak is in the file pfarraybak.h.
4  #include "pfarraybak.h"
5  #include <iostream>
6  using std::cout;
7
8  namespace PFArraySavitch
9  {
10
11  template<class T>
12  PFArrayBak<T>::PFArrayBak() : PFArray<T>(), usedB(0)
```