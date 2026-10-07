# Chapter 4 Compound Types

# Comparing Arrays, Vector Objects, and Array Objects

Perhaps the simplest way to understand the similarities and differences between arrays, vector objects, and array objects is to look at a brief example (Listing 4.24) that uses all of three approaches.

Listing 4.24 choices.cpp

```
// choices.cpp -- array variations
#include <iostream>
#include <vector> // STL C98
#include <array> // C++11
int main() {
{
    using namespace std;
    // original C++
    double a[4] = {1.2, 2.4, 3.6, 4.8};
    // C++98 STL
    vector<double> a(4); // create vector with 4 elements
    // no simple way to initialize in C98
    a[0] = 1.0/3.0;
    a[1] = 1.0/5.0;
    a[2] = 1.0/7.0;
    a[3] = 1.0/9.0;
    // C++11 -- create and initialize array object
    std::array<double, 4> a3 = {3.14, 2.72, 1.62, 1.41};
    std::array<double, 4> a4; // valid for array objects of size size
    // use notation
    cout << "a1[2]:" << a1[2] << " at " << &a1[2] << endl;
    cout << "a2[2]:" << a2[2] << " at " << &a2[2] << endl;
    cout << "a3[2]:" << a3[2] << " at " << &a3[2] << endl;
    cout << "a4[2]:" << a4[2] << " at " << &a4[2] << endl;
    // misde
    a[-2] = 20.2;
    cout << "a1[-2]:" << a1[-2] << " at " << &a1[-2] << endl;
    cout << "a3[2]:" << a3[2] << " at " << &a3[2] << endl;
    cout << "a4[2]:" << a4[2] << " at " << &a4[2] << endl;
    return 0;
}
```

Here's your sample output:

```
a1[2]: 3.6 at 0x28ccc8
a2[2]: 0.142857 at 0xca0328
a3[2]: 1.62 at 0x28ccc8
a4[2]: 1.62 at 0x28cca8
```