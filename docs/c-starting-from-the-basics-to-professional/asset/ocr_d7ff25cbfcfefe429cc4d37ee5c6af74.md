Of course, if the classes allocated free store memory and stored the address in a raw pointer, defining the class destructor would be essential to avoid memory leaks. The Carton destructor outputs the material so you can tell which Carton object is being destroyed by assigning a different material to each. Let's see how these classes behave:

```
```cpp
// Ex14_06.cpp
// Destructors in a class hierarchy
import <iostream>;
import carton;   // For the Carton class

int main()
{
    Carton carton;
    Carton candyCarton(50.0, 30.0, 20.0, "SRB");   // Solid bleached board

    std::cout << "carton volume is " << carton.volume() << std::endl;
    std::cout << "candyCarton volume is " << candyCarton.volume() << std::endl;
}
```
```

Here's the output:

```
```text
Box() called.
Carton() called.
Box(double, double, double) called.
Carton(double,double,double,string_view) called.
carton volume is 1
candyCarton volume is 30000
Carton destructor. Material = SBB
Box destructor.
Carton destructor. Material = Cardboard
Box destructor.
```
```

The point of this exercise is to see how the destructors behave. The output from the destructor calls indicates two aspects of how objects are destroyed. First, you can see the order in which destructors are called for a particular object, and second, you can see the order in which the objects are destroyed. The destructor calls recorded by the output correspond to the following actions:

| Destructor Output | Object Destroyed |
|---|---|
| Carton destructor. Material = SBB. | candyCarton object |
| Box destructor. | Box subobject of candyCarton |
| Carton destructor. Material = Cardboard. | carton object |
| Box destructor. | Box subobject of carton |

This shows that the objects that make up a derived class object are destroyed in the reverse order from which they were created. The carton object was created first and destroyed last; the candyCarton object was created last and destroyed first. This order is chosen to ensure that you never end up with an object in an illegal state. An object can be used only after it has been defined—this means that any given object can only