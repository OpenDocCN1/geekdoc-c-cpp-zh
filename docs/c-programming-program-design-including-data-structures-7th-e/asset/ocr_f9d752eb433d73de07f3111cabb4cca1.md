In the next section, we discuss how to specify a call to the constructor of the base class when writing the definition of a constructor of the derived class.

# Constructors of Derived and Base Classes

A derived class can have its own private member variables, so a derived class can explicitly include its own constructors to initialize them. When we declare a derived class object, this object inherits the members of the base class, but the derived class object cannot directly access the private (data) members of the base class. The same is true for the member functions of a derived class. That is, the member functions of a derived class cannot directly access the private members of the base class.

As a consequence, the constructors of a derived class can (directly) initialize only the (public data) members inherited from the base class of the derived class. Thus, when a derived class object is declared, it must also trigger the execution of one of the base class’s constructors. Furthermore, this triggering of the base class’s constructor is specified in the *heading of the definition* of a derived class constructor.

First, let us write the definition of the default constructor of the class boxType. Recall that, if a class contains a default constructor and no values are specified when the object is declared, the default constructor executes and initializes the object. Because the class rectangleType contains the default constructor, we do not specify any constructor of the base class when writing the definition of the default constructor of the class boxType.

```
boxType::boxType()
{
    height = 0.0;
}
```

To write the definition of class boxType constructor with parameters, we first write the class boxType constructor heading including *all of the parameters needed for both the base class and derived class constructors*; that is, all the parameters needed for both boxType and rectangleType. Then, to trigger the execution of the base class constructor with parameters, we add a colon (:) to the heading followed by the name of the constructor of the base class with its parameters in the heading of the definition of the constructor of the derived class. In effect, we “tack on” the base class constructor to the derived class constructor via a colon. The derived class constructor gets all of the parameters needed for itself and the base class constructor, then passes on the base class parameters to its constructor.