```
// array1.cpp
// note: this program will compile, but it won't link without the
// set() definition

#include <iostream>
#define SIZE 10

using namespace std;

struct intArray {
public:
    int a[SIZE];
    void set(int index, int value);
    void print();
};

void intArray::print() {
    for(int i = 0; i < SIZE; i++)
        cout << "a[" << i << "] = " << a[i] << endl;
}

int main() {
    intArray num;
    for(int i = 0; i < SIZE; i++)
        num.set(i,i);
    num.print();
}
```