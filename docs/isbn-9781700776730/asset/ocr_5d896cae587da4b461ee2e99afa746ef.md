```
// word1ldr.cpp

#include <iostream>
#include "word1ll.h"

using namespace std;

int main() {
    Word w1("Red");
    Word w2("White");
    Word w3("Blue");

    cout << w1.getCount(w1) << endl;
    cout << w2.getCount(w2) << endl;
    cout << Word::getCount(w3) << endl;
    return 0;
}
```

```
// word1ll output
Red
3
White
3
Blue
3
```

Note that you cannot declare constructors to be static. If a constructor was allowed to be static, it could be invoked without a this pointer and therefore would not be able to build objects correctly.

Remember that when you see a static member function in a class, the designer intended that function to be conceptually associated with the class as a whole. That function will have the faster calling time of an ordinary, global function, but its name will be visible only within the class so it won't clash with global function names.