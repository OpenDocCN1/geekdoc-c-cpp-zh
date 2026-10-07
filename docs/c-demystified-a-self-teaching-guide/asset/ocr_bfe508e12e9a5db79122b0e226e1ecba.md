# Indirection Operator and Dereferencing

The primary use of a pointer is to access and, if appropriate, change the value of the variable that the pointer is pointing to. In the following program, the value of the integer variable `num` is changed twice.

```
#include <iostream>
using namespace std;

int main () {
    int num = 5;
    int* IPtr = &num;
    cout << "The value of num is " << num << endl;
    num = 10;
    cout << "The value of num after num = " << num << endl;
    *IPtr = 15;
    cout << "The value of num after *IPtr is " << *IPtr << endl;
    return 0;
}
```

The resulting output is
The value of num is 5
The value of num after num = 10 is 10
The value of num after *IPtr = 15 is 15

The first change should be familiar, the direct assignment of a value to `num`, such as `num = 10`. However, the second change is accomplished a new way, using the indirection operator:
**IPtr = 15;

Note As mentioned earlier in chapter, this is an example of a symbol having different meanings in the C++ programming language depending on the context in which it was used.

The placement of the indirection operator before a pointer is to dereference the pointer. The value of a dereferenced pointer is not an address, but rather the value at that address—that is, the value that the pointer points to.

For example, in the preceding program, `IPtr`'s value is the address of `num`. However, the value of `IPtr` dereferenced is the value of `num`. Thus, the following two statements have the same effect, both changing the value of `num`:

```
num = 25;
*IPtr = 25;
```

Similarly, a dereferenced pointer can be used in arithmetic expressions the same as the