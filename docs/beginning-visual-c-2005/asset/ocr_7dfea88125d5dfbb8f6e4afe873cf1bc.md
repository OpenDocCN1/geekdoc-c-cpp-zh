```
    << " bytes" << endl
    << "myMintBox occupies " << sizeof myMintBox
    << " bytes";
    cout << endl
        << "myMintBox volume is " << myMintBox.Volume(); // Get volume of a
        // CCandyBox object
    cout << endl;
    return 0;
}
```

This example produces the following output:

```
myBox occupies 24 bytes
myCandyBox occupies 32 bytes
myMintBox occupies 32 bytes
    myMintBox volume is 1
```

# How It Works

The interesting additional output is the last line. This shows the value produced by the function Volume(), which is now in the public section of the base class. Within the derived class, it operates on the members of the derived class that are inherited from the base. It is a full member of the derived class, so it can be used freely with objects of the derived class.

The value for the volume of the derived class object is 1 because, in creating the CCandyBox object, the CBox() default constructor was called first to create the base class part of the object, and this sets default CBox dimensions to 1.

# Constructor Operation in a Derived Class

Although I said the base class constructors are not inherited in a derived class, they still exist in the base class and are used for creating the base part of a derived class object. This is because creating the base class part of a derived class object is really the business of a base class constructor, not the derived class constructor. After all, you have seen that private members of a base class are inaccessible in a derived class object, even though they are inherited, so responsibility for these has to lie with the base class constructors.

The default base class constructor was called automatically in the last example to create the base part of the derived class object, but this doesn’t have to be the case. You can arrange to call a particular base class constructor from the derived class constructor. This enables you to initialize the base class data members with a constructor other than the default, or indeed to choose to call a particular class constructor, depending on the data supplied to the derived class constructor.

# Try It Out  Calling Constructors

You can see this in action through a modified version of the previous example. To make the class usable, you really need to provide a constructor for the derived class that allows you to specify the dimensions of the object. You can add an additional constructor in the derived class to do this, and call the base class constructor explicitly to set the values of the data members that are inherited from the base class.