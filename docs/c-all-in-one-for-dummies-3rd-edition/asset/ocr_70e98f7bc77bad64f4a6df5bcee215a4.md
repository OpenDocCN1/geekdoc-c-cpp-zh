Each brand has certain characteristics that might be unique to it, but each has all the characteristics of class Vehicle. That’s called *inheritance*. The class Toyota, for example, has all the characteristics found in Vehicle. And the class Prius has all the characteristics found in Toyota, which includes those inherited from Vehicle.

# ### Creating a hierarchy in C++

In C++, you can create a hierarchy of classes. When you take one class and create a new one under it, such as creating Toyota from Vehicle, you are *deriving* a new class.

To derive a class from an existing class, you write the new class as you would any other class, but you extend the header after the class name with a colon, :, the word public, and then the class you’re deriving from, as in the following class header line:

```
~~~cpp
class Toyota : public Vehicle {
~~~
```

When you do so, the class you create (Toyota) inherits the member variables and functions from the previous class (Vehicle). For example, if Vehicle has a public member variable called NumberOfWheels and a public member function called Drive, the class Toyota has these members, although you didn’t write the members in Toyota.

The VehicleClass example shown in Listing 8-12 demonstrates class inheritance. We started with a class called Vehicle, and we derived a class called Toyota. In main( ), we create an instance of Toyota, and we call two member functions for the instance, MeAndMyToyota( ) and Drive( ). The definition of the Toyota class does not show a Drive( ) function. The Drive( ) function is inherited from the Vehicle class. You can call this function like a member of the Toyota class because in many ways it is.

# ### Listing 8-12: Deriving One Class from Another

```
~~~cpp
#include <iostream>

using namespace std;

class Vehicle
{
public:
    int NumberOfWheels;

    void Drive()
    {
        cout << "Driving, driving, driving..." << endl;
    }
};
~~~
```

(continued)