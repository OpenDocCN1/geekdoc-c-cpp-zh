We'll often find that all of the members of the class can be so initialized, and by the time we get to the body of the constructor, there is nothing left to do. This is a good sign. Your constructor has initialized all of its members with the correct initialization values.

Also note that the initialization syntax allows us to initialize data members that are not class objects. Built-in types have no constructor, initializing the integer member id using the initialization syntax is no faster than using assignment. But the code is easier to read if we initialize all of the data members in the same way.

Here is the complete program using the constructor initializer lists: 

```
// contain2.cpp
#include <iostream>
#include <string.h>

using namespace std;

class String {
private:
    char *buf;
public:
    String() {
        cout << "String default constructor" << endl;
        buf = new char[strlen("Shari")+1];
        strcpy(buf, "Shari");
    }
    String(char *s) {
        cout << "String one arg constructor" << endl;
        buf = new char[strlen(s)+1];
        strcpy(buf, s);
    }
    ~String() {
        delete [] buf;
    }
    void printString() {
        cout << buf << endl;
    }
}
;
```