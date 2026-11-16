# Static Member Functions

Suppose you want to read or modify a `static` data member. You can access a `static` data member just like any other member by using a normal member function like this:

```
// word6.h

#ifndef _WORD6_H
#define _WORD6_H

class Word {
 private:
   char *buf;
   static int wordCount;
 public:
   Word(char *s);
   int getCount();
};

#endif

// word6.cpp

#include <string.h>
#include "word6.h"

int Word::wordCount = 0;

Word::Word(char *s) {
  buf = strdup(s);
  wordCount++;
}

int Word::getCount() {
  return wordCount;
}
```