```
```cpp
#include <string>
#include <iostream>
using namespace std;
#include "console.h"
int main() {
string small, large;
small = "I am short";
large = "I, friend, am a long and elaborate
string indeed";
cout << "The short string is " << small.length()
<< " characters." << endl;
cout << "The long string is " << large.length()
<< " characters." << endl;
return 0;
}
output:
The short string is 10 characters.
The long string is 48 characters.
```
```

# Individual character access.

Using square brackets, you can access individual characters within a string as if it were a char array. Within string str, positions are numbered from 0 to str.length() - 1. [] can be used to read and to write characters within a string.

example program: