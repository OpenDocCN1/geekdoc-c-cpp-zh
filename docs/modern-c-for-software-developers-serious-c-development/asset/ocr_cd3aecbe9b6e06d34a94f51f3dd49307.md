answer is that it depends upon how p is declared.

Consider this program:

```
#include <iostream>
using namespace std;

// forward declarations
int myfunc(int a);
int myfunc(int a, int b);

int main() {
    // pointer to a function with declaration int f(int)
    int (*fp)(int);             // points to myfunc
    fp = myfunc;

    cout << fp(5) << endl;

    // pointer to a function with declaration int f(int, int)
    int (*f)(int, int);
    f = myfunc;

    cout << f(5, 6) << endl;
}

int myfunc(int a) {
    return a;
}

int myfunc(int a, int b) {
    return a*b;
}

// output
5
30
```

Here, there are two versions of myfunc(). Both return an int, but one takes a single integer argument and the other requires two integer arguments. In this program, fp is declared as a pointer to a function that takes one integer argument and returns an integer. When fp is assigned the address of myfunc(), C++ uses this information to select