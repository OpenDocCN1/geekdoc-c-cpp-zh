This produces the following output:

```
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

```
    Carton(const Carton& carton) : Box{carton}, m_material{carton.m_material}
    { std::cout << "Carton copy constructor" << std::endl; }
```

The Box copy constructor is called with the carton object as an argument. The carton object is of type Carton, but it is also a perfectly good Box object. The parameter for the Box class copy constructor is a reference to a Box object, so the compiler will pass carton as type Box&, which will result in only the base part of carton being passed to the Box copy constructor. If you compile and run the example again, the output will be as follows:

```
    Box(double, double, double) called.
    Carton(double,double,double,string_view) called.
    
    Box copy constructor
    Carton copy constructor
    
    Volume of carton is 24000
    Volume of cartonCopy is 24000
```

The output shows that the constructors are called in the correct order. In particular, the Box copy constructor initializes the Box subobject of carton before the body of the Carton copy constructor is entered. By way of a check, you can see that the volumes of the carton and cartonCopy objects are now identical.