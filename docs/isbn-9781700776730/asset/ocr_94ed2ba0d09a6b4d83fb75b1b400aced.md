# Static Homework

1. Add a destructor to the Word5 class below which decrements wordCount. Create a driver for your code and show that your destructor works.

```
// word5.h
#ifndef WORD5_H
#define WORD5_H

class Word {
private:
    char *buf;
    static int wordCount;
public:
    Word(char *s);
    int getCount();
};

#endif

// word5.cpp
#include <string.h>
#include "word5.h"

int Word::wordCount = 0;

Word::Word(char *s) {
    buf = strdup(s); // might need to use _strdup(s) here
    wordCount++;
}

int Word::getCount() {
    return wordCount;
}
```

2. Write some code that shows the this pointer is successfully passed into normal member functions but cannot be accessed within static member functions.