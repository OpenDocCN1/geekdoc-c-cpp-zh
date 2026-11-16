# Concatenating String with + Operator

Consider the following `String` class:

```
const int SIZE = 100;
#include <iostream>
#include <string.h>
using namespace std;
class String {
private:
    char buf[SIZE];
public:
    String() { buf[0] = '\0'; }
    String(char s[]) { strcpy(buf, s); }
    void display() { cout << buf; }
    String operator+(String s);
};
String String::operator+(String s) {
    if (strlen(buf) + strlen(s.buf) < SIZE) {
        String temp;
        strcpy(temp.buf, buf);
        strcat(temp.buf, s.buf);
        return temp;
    }
    else
        return String(); // returns NULL String
}
int main() {
    String s1 = "Hello ", s2 = "world! ", s3;
    s3 = s1 + s2;
    s3.display();
    return 0;
}
output:
Hello world!
```

The + operator takes one argument of type `String` and returns an object of type `String`.