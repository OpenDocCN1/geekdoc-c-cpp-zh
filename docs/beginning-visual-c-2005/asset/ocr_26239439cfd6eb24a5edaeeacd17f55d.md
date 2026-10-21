This is a simple property that makes available the units assumed by the class as a string. You access a static property by qualifying the property name with the name of the class, just as you would any other static member of the class:

```
Console::WriteLine(L"Class units are {0}.", Length::Units);
```

Static class properties exist whether or not any objects of the class type have been created. This differs from instance properties, which are specific to each object of the class type. Of course, if you have defined a class object, you can access a static property using the variable name. If you have created a Length object with the name len for example, you could output the value of the static Units property with the statement:

```
Console::WriteLine(L"Class units are {0}.", len.Units);
```

For accessing a static property in a reference class through a handle to an object of that type you would use the -> operator.

# Reserved Property Names

Although properties are different from fields, the values for properties still have to be stored somewhere and the storage locations need to be identified somehow. Internally properties have names created for the storage locations that are needed, and such names are reserved in a class that has properties so you must not use these names for other purposes.

If you define a scalar or named indexed property with the name NAME in a class, the names get_NAME and set_NAME are reserved in the class so you must not use them for other purposes. Both names are reserved regardless of whether or not you define the get() and set() functions for the property. When you define a default indexed property in a class, the names get_Item and set_Item are reserved. The possibility of there being reserved names that use underscore characters is a good reason for avoiding the use of the underscore character in your own names in a C++/CLI program.

# initonly Fields

Literal fields are a convenient way of introducing constants into a class, but they have the limitation that their values must be defined when you compile the program. C++/CLI also provides initonly fields in a class that are constants that you can initialize in a constructor. Here’s an example of an initonly field in a skeleton version of the Length class:

```
value class Length
{
private:
    int feet;
    int inches;

public:
    initonly int inchesPerFoot;              // initonly field

    // Constructor
    Length(int ft, int ins) :
            feet(ft), inches(ins),              // Initialize fields
            inchesPerFoot(12)                   // Initialize initonly field
    {}
};
```