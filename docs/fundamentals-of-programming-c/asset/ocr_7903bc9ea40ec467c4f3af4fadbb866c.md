# 19.2. EXCEPTION EXAMPLES

event, and the program should handle it part of its normal processing.

An exception almost always represents a problem, usually some run-time error. Suppose we have a vector v and an integer i. Unless 0 <= i < v.size(), the expression v[i] attempts to access the outside element of the vector. The operator[] performs no bounds checking; thus an executing using the expression v[i] could produce undefined behavior. Consider instead the expression v.at(i). The method works just like operator[], except at do check the vector's bounds. If i >= v.size() or i < 0, the expression v.at(i) represents an exceptional situation, and we say the vector's method throws, or raises, an exception.

Without advantage of C++ exception handling infrastructure, the following statement:

```
v.at(i) = 4;
```

could terminate the program with an error message. This is better than without undefined behavior, it is not ideal. The program crashes. When a real application crashes the user may lose data. Badly behaving programs terminate unexpectedly. It would be better to defend against the out-of-bounds index and keep the program alive.

 algorithm could help many potential problems solved. For example, a programmer can use an if statement to see if a vector's index is within the proper bounds:

```
if (0 < i && i < v.size()) // Ensure i is in range
v.at(i) = 4;
```

However, if the program accesses a vector in several different locations within a function and the index variable can change from place to place, the if statements necessary to ensure safe access might miss the overall logic of the function or method.

# 19.2 Exception Examples

> CAUTION! SECTION UNDER CONSTRUCTION

Consider Listing 19.1 (vectorboundscrash.cpp). The program crashes whenever the user enters an index out of the range of vector `nums`.

Listing 19.1: vectorboundscrash.cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<double> nums { 1.0, 2.0, 3.0 };
    int input;
    cout << "Enter index: ";
    cin >> input;
    cout << nums.at(input) << endl;
}

The method guarantees that an illegal access will not go undetected. To intercept the problem at time and prevent the program from terminating due to an error, we use a try/catch block, which consists of two parts: a try block and a catch block. To form a try/catch block we