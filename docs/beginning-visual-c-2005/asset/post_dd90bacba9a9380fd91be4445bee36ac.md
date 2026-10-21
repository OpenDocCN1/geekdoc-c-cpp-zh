
```
<< "Volume of box1 = " << boxVolume;
```

```
box2.m_Height = box1.m_Height - 10;  // Define box2
box2.m_Length = box1.m_Length / 2.0;  // members in
box2.m_Width = 0.25*box1.m_Length;    // terms of box1

cout << endl
    << "Volume of box2 = "
    << box2.Volume();
```

```
cout << endl
    << "Volume of cigarBox = "
    << cigarBox.Volume();

cout << endl;
return 0;
}
```

## How It Works

Now that you have included your own version of the default constructor, there are no error messages from the compiler and everything works. The program produces this output:

```
Constructor called.
Default constructor called.
Constructor called.
Volume of box1 = 33696
Volume of box2 = 6084
Volume of cigarBox = 40
```

All that the default constructor does is display a message. Evidently, it was called when you declared the object box2. You also get the correct value for the volumes of all three CBox objects, so the rest of the program is working as it should.

One aspect of this example that you may have noticed is that you now know we can overload constructors just as you overloaded functions in Chapter 6. You have just executed an example with two constructors that differ only in their parameter list. One has three parameters of type double and the other has no parameters at all.

## Assigning Default Parameter Values in a Class

When discussing functions, you saw how you could specify default values for the parameters to a function in the function prototype. You can also do this for class member functions, including constructors. If you put the definition of the member function inside the class definition, you can put the default values for the parameters in the function header. If you include only the prototype of a function in the class definition, the default parameter values should go in the prototype.

If you decided that the default size for a CBox object was a unit box with all sides of length 1, you could alter the class definition in the last example to this:

```
class CBox                 // Class definition at global scope
{
    public:
```

```
double m_Length;                         // Length of a box in inches
 double m_Width;                          // Width of a box in inches
 double m_Height;                         // Height of a box in inches

 // Constructor definition
 CBox(double lv = 1.0, double bv = 1.0, double hv = 1.0)
 {
     cout << endl << "Constructor called.";
     m_Length = lv;                       // Set values of
     m_Width = bv;                        // data members
     m_Height = hv;
 }

 // Default constructor definition
 CBox()
 {
     cout << endl << "Default constructor called.";
 }

 // Function to calculate the volume of a box
 double Volume()
 {
     return m_Length*m_Width*m_Height;
 }
};
```

If you make this change to the last example, what happens? You get another error message from the compiler, of course. Amongst a lot of other stuff, you get these useful comments from the compiler:

```
warning C4520: 'CBox': multiple default constructors specified
error C2668: 'CBox::CBox': ambiguous call to overloaded function
```

This means that the compiler can’t work out which of the two constructors to call—the one for which you have set default values for the parameters or the constructor that doesn’t accept any parameters. This is because the declaration of box2 requires a constructor without parameters and either constructor can now be called without parameters. The immediately obvious solution to this is to get rid of the constructor that accepts no parameters. This is actually beneficial. Without this constructor, any CBox object declared without being explicitly initialized will automatically have its members initialized to 1.

## Try It Out    Supplying Default Values for Constructor Arguments

You can demonstrate this with the following simplified example:

```
// Ex7_06.cpp
// Supplying default values for constructor arguments
#include <iostream>
using std::cout;
using std::endl;

class CBox                              // Class definition at global scope
{
public:
    double m_Length;                     // Length of a box in inches
```

```
double m_Width;                  // Width of a box in inches
double m_Height;                 // Height of a box in inches

// Constructor definition
CBox(double lv = 1.0, double bv = 1.0, double hv = 1.0)
{
    cout << endl << "Constructor called.";
    m_Length = lv;                 // Set values of
    m_Width = bv;                  // data members
    m_Height = hv;
}

// Function to calculate the volume of a box
double Volume()
{
    return m_Length*m_Width*m_Height;
}
};

int main()
{
    CBox box2;                      // Declare box2 - no initial values

    cout << endl
         << "Volume of box2 = "
         << box2.Volume();

    cout << endl;
    return 0;
}
```

## How It Works

You only declare a single uninitialized CBox variable— box2 —because that’s all you need for demonstration purposes. This version of the program produces the following output:

```
Constructor called.
Volume of box2 = 1
```

This shows that the constructor with default parameter values is doing its job of setting the values of objects that have no initializing values specified.

You should not assume from this that this is the only, or even the recommended, way of implementing the default constructor. There will be many occasions where you won’t want to assign default values in this way, in which case you’ll need to write a separate default constructor. There will even be times when you don’t want to have a default constructor operating at all, even though you have defined another constructor. This would ensure that all declared objects of a class must have initializing values explicitly specified in their declaration.

## Using an Initialization List in a Constructor

Previously, you initialized the members of an object in the class constructor using explicit assignment. You could also have used a different technique, using what is called an initialization list. I can demonstrate this with an alternative version of the constructor for the class CBox:

```
// Constructor definition using an initialization list
CBox(double lv = 1.0, double bv = 1.0, double hv = 1.0):
    m_Length(lv), m_Width(bv), m_Height(hv)
{
    cout << endl << "Constructor called.";
}
```

The way this constructor definition is written assumes that it appears within the body of the class definition. Now the values of the data members are not set in assignment statements in the body of the constructor. As in a declaration, they are specified as initializing values using functional notation and appear in the initializing list as part of the function header. The member m_Length is initialized by the value of lv, for example. This can be more efficient than using assignments as you did in the previous version. If you substitute this version of the constructor in the previous example, you will see that it works just as well.

Note that the initializing list for the constructor is separated from the parameter list by a colon and each of the initializers is separated by a comma. This technique for initializing parameters in a constructor is important, because, as you will see later, it's the only way of setting values for certain types of data members of an object. The MFC also rely heavily on the initialization list technique.

## Private Members of a Class

Having a constructor that sets the values of the data members of a class object but still admits the possibility of any part of a program being able to mess with what are essentially the guts of an object is almost a contradiction in terms. To draw an analogy, after you have arranged for a brilliant surgeon such as Dr. Kildare, whose skills were honed over years of training, to do things to your insides, letting the local plumber or bricklayer have a go hardly seems appropriate. You need some protection for your class data members.

You can get the security you need by using the keyword private when you define the class members. Class members that are private can, in general, be accessed only by member functions of a class. There's one exception, but we'll worry about that later. A normal function has no direct means of accessing the private members of a class. This is shown in Figure 7-6.

Having the possibility of specifying class members as private also enables you to separate the interface to the class from its internal implementation. The interface to a class is composed of the public members and the public member functions in particular because they can provide indirect access to all the members of a class, including the private members. By keeping the internals of a class private, you can later modify them to improve performance for example without necessitating modifications to the code that uses the class through its public interface. To keep data and function members of a class safe from unnecessary meddling, it's good practice to declare those that don't need to be exposed as private. Only make public what is essential to the use of your class.
