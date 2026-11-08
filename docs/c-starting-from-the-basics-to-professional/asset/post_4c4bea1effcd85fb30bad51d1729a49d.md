
```cpp
Carton(double l, double w, double h, std::string_view material)
    : Box{l, w, h, material}
    { std::cout << "Carton(double,double,double,string_view) called.\n"; }

private:
    std::string m_material {"Cardboard"};
};
```

This class has four constructors, including a default constructor. You must define this here because if you define any constructor, the compiler will not supply a default constructor. As always, we declare our single-argument constructor to be explicit to avoid unwanted implicit conversions.

> **Note**  The notation for calling the base class constructor is the same as that used for initializing member variables in a constructor. This is perfectly consistent: You are essentially initializing the Box subobject of the Carton object using the arguments passed to the Carton constructor.

Here’s the code to exercise the derived Carton class:

```cpp
// Ex14_02.cpp
// Calling base class constructors in a derived class constructor
import <iostream>;
import carton;              // for the Carton class

int main()
{
    // Create four Carton objects
    Carton carton1;                         std::cout << std::endl;
    Carton carton2 {"White-chipboard"};    std::cout << std::endl;
    Carton carton3 {4.0, 5.0, 6.0, "PTE"}; std::cout << std::endl;
    Carton carton4 {2.0, "Folding boxboard"}; std::cout << std::endl;

    std::cout << "carton1 volume is " << carton1.volume() << std::endl;
    std::cout << "carton2 volume is " << carton2.volume() << std::endl;
    std::cout << "carton3 volume is " << carton3.volume() << std::endl;
    std::cout << "carton4 volume is " << carton4.volume() << std::endl;
}
```

The output is as follows:

```text
Box() called.
Carton() called.

Box() called.
Carton(string_view) called.

Box(double, double, double) called.
Carton(double,double,double,string_view) called.
Box(double, double, double) called.
Box(double) called.
Carton(double,string_view) called.

carton1 volume is 1
carton2 volume is 1
carton3 volume is 120
carton4 volume is 8
```

The output shows which constructors are evaluated for each of the four Carton objects that are created in main():

- Creating the first Carton object, carton1, results in the default constructor for the Box class being evaluated first, followed by the default constructor for the Carton class.
- Creating carton2 evaluates the default constructor of Box followed by the Carton constructor with a string_view parameter.
- Creating the carton3 object evaluates the Box constructor with three parameters followed by the Carton constructor with four parameters.
- Creating carton4 causes two Box constructors to be called because the Box constructor with a single parameter of type double that is called by the Carton constructor calls the Box constructor with three parameters in its initialization list.

This is all consistent with constructors being evaluated in sequence from the most base to the most derived. Every derived class constructor calls a base class constructor. If a user-defined derived class constructor does not explicitly call a base class constructor in its initialization list, the default constructor will be called.

You can never initialize member variables of a base class in the initialization list for a derived class' constructor. Not even if those members are protected or public. For example, try replacing the fourth and last Carton class constructor in Ex14_02 with the following:

```cpp
// This constructor won't compile!
Carton::Carton(double l, double w, double h, std::string_view material)
    : m_length{l}, m_width{w}, m_height{h}, m_material{material}
{
    std::cout << "Carton(double,double,double,string_view) called.\n";
}
```

You might expect this to work because m_length, m_width, and m_height are protected base class members that are inherited publicly, so the Carton class constructor should be able to access them. However, the compiler will complain that m_length, m_width, and m_height are not members of the Carton class. This will be the case even if you make the member variables of the Box class public. If you want to initialize the inherited member variables explicitly, you could in the initialization list or the body of the derived class constructor. The following constructor definition would compile:

```cpp
// Constructor that will compile
Carton::Carton(double l, double w, double h, std::string_view material)
    : m_material{material}
{
    m_length = l;   // These should normally be initialized in a base class constructor...
    m_width = w;
    m_height = h;
    std::cout << "Carton(double,double,double,string_view) called.\n";
}
```

This produces the following output:

```text
    Box(double, double, double) called.
    Carton(double,double,double,string_view) called.
    
    Box() called.
    Carton copy constructor
    
    Volume of carton is 24000
    Volume of cartonCopy is 1
```

All is not as it should be. Clearly the volume of cartonCopy isn't the same as carton, but the output also shows the reason for this. To copy the carton object, you call the copy constructor for the Carton class. The Carton copy constructor should make a copy of the Box subobject of carton, and to do this it should call the Box copy constructor. However, the output clearly shows that the default Box constructor is being called instead.

The Carton copy constructor won't call the Box copy constructor if you don't tell it to do so. The compiler knows that it has to create a Box subobject for the object carton, but if you don't specify how, the compiler won't second-guess your intentions—it will just create a default base object.

The obvious fix for this is to call the Box copy constructor in the initialization list of the Carton copy constructor. Simply change the copy constructor definition to this:

```cpp
    Carton(const Carton& carton) : Box{carton}, m_material{carton.m_material}
    { std::cout << "Carton copy constructor" << std::endl; }
```

The Box copy constructor is called with the carton object as an argument. The carton object is of type Carton, but it is also a perfectly good Box object. The parameter for the Box class copy constructor is a reference to a Box object, so the compiler will pass carton as type Box&, which will result in only the base part of carton being passed to the Box copy constructor. If you compile and run the example again, the output will be as follows:

```text
    Box(double, double, double) called.
    Carton(double,double,double,string_view) called.
    
    Box copy constructor
    Carton copy constructor
    
    Volume of carton is 24000
    Volume of cartonCopy is 24000
```

The output shows that the constructors are called in the correct order. In particular, the Box copy constructor initializes the Box subobject of carton before the body of the Carton copy constructor is entered. By way of a check, you can see that the volumes of the carton and cartonCopy objects are now identical.

## The Default Constructor in a Derived Class

You know that the compiler will not supply a default constructor if you define one or more constructors for a class. You also know that you can tell the compiler to insert a default constructor in any event using the default keyword. You could replace the definition of the default constructor in the Carton class definition in Ex14_02 with this statement:

```cpp
Carton() = default;
```

Now the compiler will supply a definition, even though you have defined other constructors. The definition that the compiler supplies for a derived class calls the base class constructor, so it looks like this:

```cpp
Carton() : Box{} {};
```

If the base class does not have a non-private default constructor, or if its default constructor is deleted (either implicitly or explicitly using = delete), then a defaulted default constructor of the derived class shall be implicitly deleted. In other words, adding = default to the derived class then has the same effect as adding = delete.

To demonstrate this you can take the following steps. Start from Ex14_02. Begin by replacing the default constructor of the Carton class with Carton() = default; (as suggested earlier) and removing the explicit constructor of Carton that accepts a string_view (which also relies on the default constructor of Box). Next, remove the line in the main() program that calls the latter constructor, but be sure to keep the line that default-constructs a Carton. After that, you can alter the default constructor from the Box class in one of three ways: you either remove it, replace it with Box() = delete;, or make it private. In any case, the Carton class and Carton module will continue to compile just fine (even with the defaulted default constructor), but the default construction of Carton in the main() function will result in a compilation error. This error should normally inform you that your defaulted default constructor for Carton is indeed implicitly deleted.

The different variations of Ex14_02 discussed in this section are available online as Ex14_04, Ex14_04A, Ex14_04B, and Ex14_04C.

## Inheriting Constructors

Base class constructors are not normally inherited in a derived class. This is because a derived class typically has additional member variables that need to be initialized, and a base class constructor would have no knowledge of these. However, you can cause constructors to be inherited from a direct base class by putting a using declaration in the derived class. Here's how a version of the Carton class from Ex14_02 could be made to inherit the Box class constructors:

```cpp
class Carton : public Box
{
    using Box::Box; // Inherit Box class constructors

public:
    Carton(double length, double width, double height, std::string_view mat)
        : Box{length, width, height}, m_material{mat}
    { std::cout << "Carton(double,double,double,string_view) called.\n"; }

private:
    std::string m_material {"Cardboard"};
};
```
