C++ allows you to surmount these problems in an elegant fashion. You can define a member function as static! This meaning is close to the one for static data members, i.e., the function is for the whole class and not just one object of the class.

The key is that the this pointer is not secretly passed into a static member function. However, you also cannot access anything but static data members and static member functions.

Since a function is a member of the class, its name is hidden inside the scope of the class and will not collide with global names. In addition, you have the notational convenience of associating the name of the class, so it's more obvious what the function is supposed to do and that it may be affected by changes in the class.

```
// word8.h

#ifndef WORD8_H
#define WORD8_H

class Word {
    private:
        char *buf;
        static int wordCount;
    public:
        Word(char *s);
        static int getCount();
};

#endif
```

```
// word8.cpp

#include <string.h>
#include "word8.h"

int Word::wordCount = 0;

Word::Word(char *s) {
    buf = strdup(s);
    wordCount++;
}

int Word::getCount() {
    return wordCount;
}
```