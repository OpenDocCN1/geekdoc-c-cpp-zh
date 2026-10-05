```
#include <iostream>
#include <compare>
using namespace std;

template<typename T>
struct MyObject {
    T value;
    MyObject(T val) : value(val) {}
    bool operator<>(const MyObject& rhs) = default;
};

int main() {
    MyObject<float> object1(10.5), object2(30.4);
    bool ret = object1.value < object2.value;
    cout << boolalpha << ret << endl;

    MyObject<const char*> strobej1("hello"), strobej2("hello");
    ret = strobej1.value < strobej2.value;
    cout << boolalpha << ret << endl;
}

// output
true
false
```