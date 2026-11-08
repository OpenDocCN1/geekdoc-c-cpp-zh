```
```cpp
std::vector<const Vessel*> vessels {&box, &can, &carton, &hardcase};

for (const auto* vessel : vessels)
    std::cout << "Volume is " << vessel->volume() << std::endl;
}
```
```

This generates the following output:

```
```
Volume is 24000
Volume is 235.619
Volume is 2272.4
Volume is 20400
```
```

This time around, we used a vector of raw pointers to Vessel objects to exercise the virtual functions. The output shows that all the polymorphic calls of the `volume()` function work as expected. You have a three-level class hierarchy in this example, as shown in Figure 15-8.

![](bbox=[0.169, 0.42, 0.68, 0.669])

*Figure 15-8. A three-level class hierarchy*

Recall that if a derived class fails to define a function that’s declared as a pure virtual function in the base class, then the function will be inherited as a pure virtual function, and this will make the derived class an abstract class. You can demonstrate this effect by removing the const declaration from either the Can or the Box class. This makes the function different from the pure virtual function in the base class, so the derived class inherits the base class version, and the program won’t compile.