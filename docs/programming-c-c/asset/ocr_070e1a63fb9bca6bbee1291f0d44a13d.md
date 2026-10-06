![](bbox=[0.343, 0.178, 0.656, 0.342])

# C++ Program to Implement Hierarchical Inheritance

```
#include <iostream>
using namespace std;

// base class
class Vehicle
{
public:
    Vehicle()
    {
        cout << "This is a Vehicle" << endl;
    }
}

// first sub class
class Car: public Vehicle
{
}

// second sub class
class Bus: public Vehicle
{
```