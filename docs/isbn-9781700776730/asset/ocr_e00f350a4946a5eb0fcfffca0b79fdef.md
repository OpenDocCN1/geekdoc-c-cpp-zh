```
// farrayl.cpp - friend function
// note: this program will compile, but it won't link without
// the set() definition

#include <iostream>
#define SIZE 10

using namespace std;

struct intArray {
private:
    int a[SIZE];
public:
    void set(int index, int value);
    friend void print(intArray);
};

void print(intArray x) {
    for(int i = 0; i < SIZE; i++)
        cout << "a[" << i << "] = " << x.a[i] << endl;
}

int main() {
    intArray num;

    for(int i = 0; i < SIZE; i++)
        num.set(i,i);
    print(num);
}
```

```
// employee.cpp - entire structs can be friends

using namespace std;

struct employee {
private:
    int salary;
    int benefitLevel;
public:
    void initialize(int startingPay);
    void raise(float percent);
    friend struct accountant;
};

int main() {
    // code not fully shown in snippet
}
```