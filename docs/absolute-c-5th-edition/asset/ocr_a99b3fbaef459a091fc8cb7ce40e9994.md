# CHAPTER 16 Templates

Display 16.8 Interface for the Template Class PFArrayBak

```
//This is the header file parraybak.h. This is the interface for the
// template class PFArrayBak. Objects of this type are partially filled
// arrays of any type T. This version allows the programmer to make a
// backup copy and restore to the last saved copy of the partially filled
// array.
#ifndef PFRAYBAK_H
#define PFRAYBAK_H
#include "pfarraybak.h"

namespace PFArraySavitch {
    template<class T>
    class PFArrayBak : public PFArray<T> {
    public:
        PFArrayBak();
        //Initializes with a capacity of 50.

        PFArrayBak(const PFArrayBak<T>& Object);

        void backup();
        //Makes a backup of the partially filled array.

        void restore();
        //Restores the partially filled array to the last saved version.
        //If array has never been invoked, this empties the partially
        // array.

        PFArrayBak<T>& operator=(const PFArrayBak<T>& rightSide);
        virtual ~PFArrayBak();
    private:
        T* bck; //for a backup of main array.
        int usedb; //for inherited member variable used.
    };
}
#endif
```

Display 16.9 Implementation for the Template Class PFArrayBak (part 1 of 3)

```
//This is the file parraybak.cpp.
//This is the implementation for the template class PFArrayBak. The
//interface for the template class PFArrayBak is in the file
//pfarraybak.h.
#include "pfarraybak.h"
#include <iostream>
```