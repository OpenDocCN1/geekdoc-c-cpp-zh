```
// word7.cpp
#include <string.h>
#include "word7.h"

int Word::wordCount = 0;

Word::Word(char *s) {
    buf = strdup(s);
    wordCount++;
}

int getCount() {
    return Word::wordCount;
}

// word7drv.cpp
#include <iostream>
#include "word7.h"

using namespace std;

int main() {
    Word w1("Red");
    Word w2("White");
    Word w3("Blue");
    Return 0;

    cout << getCount() << endl;
}

// word7 output
```

We are now defined getCount() outside the class as:

```
int getCount() {
    return Word::wordCount;
}
```

getCount() is a global function which has access to static private data, but it doesn't have the overhead. However the function is no longer in the scope of class Word. So if someone introduces the name getCount() by bringing in another library, for example, there will be a clash.