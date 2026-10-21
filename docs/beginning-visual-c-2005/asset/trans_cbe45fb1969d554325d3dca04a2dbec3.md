

The example produces the following output:

```
Constructor called.
Constructor called.
Volume of match = 1.21
Surface area of match = 8.14
Volume of box2 = 1
Surface area of box2 = 6
```

This is exactly what you would expect. The friend function is computing the surface area of the CBox objects from the values of the private members.

## Placing friend Function Definitions Inside the Class

You could have combined the definition of the function with its declaration as a friend of the CBox class within the class definition and the code would run as before. The function definition in the class would be:

```
friend double BoxSurface(CBox aBox)
{
    return 2.0*(aBox.m_Length*aBox.m_Width +
        aBox.m_Length*aBox.m_Height +
        aBox.m_Height*aBox.m_Width);
}
```

However, this has a number of disadvantages relating to the readability of the code. Although the function would still have global scope, this might not be obvious to readers of the code, because the function would be hidden in the body of the class definition.

## The Default Copy Constructor

Suppose that you declare and initialize a CBox object box1 with this statement:

```
CBox box1(78.0, 24.0, 18.0);
```

You now want to create another CBox object, identical to the first. You would like to initialize the second CBox object with box1. Let’s try it.

### Try It Out   Copying Information Between Instances

The following example shows this in action:

```
// Ex7_09.cpp
// Initializing an object with an object of the same class
#include <iostream>
using std::cout;
using std::endl;

class CBox                 // Class definition at global scope
{
public:
    // Constructor definition
CBox(double lv = 1.0, double bv = 1.0, double hv = 1.0)
{
    cout << endl << "Constructor called.";
    m_Length = lv;                // Set values of
    m_Width = bv;                 // data members
    m_Height = hv;
}

// Function to calculate the volume of a box
double Volume()
{
    return m_Length*m_Width*m_Height;
}

private:
    double m_Length;              // Length of a box in inches
    double m_Width;               // Width of a box in inches
    double m_Height;              // Height of a box in inches
};

int main()
{
    CBox box1(78.0, 24.0, 18.0);
    CBox box2 = box1;             // Initialize box2 with box1

    cout << endl
         << "box1 volume = " << box1.Volume()
         << endl
         << "box2 volume = " << box2.Volume();

    cout << endl;
    return 0;
}
```

This example produces the following output:

```
Constructor called.
box1 volume = 33696
box2 volume = 33696
```

### How It Works

Clearly, the program is working as you would want, with both boxes having the same volume. However, as you can see from the output, our constructor was called only once for the creation of box1. The question is, how was box2 created? The mechanism is similar to the one that you experienced when you had no constructor defined and the compiler supplied a default constructor to allow an object to be created. In this case, the compiler generates a default version of what is referred to as a copy constructor.

A copy constructor does exactly what we’re doing here — it creates an object of a class by initializing it with an existing object of the same class. The default version of the copy constructor creates the new object by copying the existing object, member by member.

This is fine for simple classes such as CBox, but for many classes — classes that have pointers or arrays as members for example — it won’t work properly. Indeed, with such classes the default copy constructor can create serious errors in your program. In these cases, you must create your own class copy constructor. This requires a special approach that you’ll look into more fully towards the end of this chapter and again in the next chapter.

## The Pointer this

In the CBox class, you wrote the Volume() function in terms of the class member names in the definition of the class. Of course, every object of type CBox that you create contains these members so there has to be a mechanism for the function to refer to the members of the particular object for which the function is called.

When any member function executes, it automatically contains a hidden pointer with the name this, which points to the object used with the function call. Therefore, when the member m_Length is accessed in the Volume() function during execution, it’s actually referring to this->m_Length, which is the fully-specified reference to the object member that is being used. The compiler takes care of adding the necessary pointer name this to the member names in the function.

If you need to, you can use the pointer this explicitly within a member function. You might, for example, want to return a pointer to the current object.

### Try It Out   Explicit Use of this

You could add a public function to the CBox class that compares the volume of two CBox objects.

```
// Ex7_10.cpp
// Using the pointer this
#include <iostream>
using std::cout;
using std::endl;

class CBox            // Class definition at global scope
{
public:
    // Constructor definition
    CBox(double lv = 1.0, double bv = 1.0, double hv = 1.0)
    {
        cout << endl << "Constructor called.";
        m_Length = lv;                // Set values of
        m_Width = bv;                 // data members
        m_Height = hv;
    }

    // Function to calculate the volume of a box
    double Volume()
    {
        return m_Length*m_Width*m_Height;
    }

// Function to compare two boxes which returns true (1)
// if the first is greater than the second, and false (0) otherwise
int Compare(CBox xBox)
{
    return this->Volume() > xBox.Volume();
}
```

```
private:
    double m_Length;                // Length of a box in inches
    double m_Width;                 // Width of a box in inches
    double m_Height;                // Height of a box in inches
};
```

```
int main()
{
    CBox match(2.2, 1.1, 0.5);       // Declare match box
    CBox cigar(8.0, 5.0,1.0);        // Declare cigar box

    if(cigar.Compare(match))
        cout << endl
             << "match is smaller than cigar";
    else
        cout << endl
             << "match is equal to or larger than cigar";

    cout << endl;
    return 0;
}
```

### How It Works

The member function Compare() returns true if the prefixed CBox object in the function call has a greater volume than the CBox object specified as an argument, and false if it doesn’t. In the return statements, the prefixed object is referred to through the pointer this, used with the indirect member access operator, ->, that you saw earlier in this chapter.

> Remember that you use the direct member access operator when accessing members through objects and the indirect member access operator when accessing members through pointers to objects. this is a pointer so you use the -> operator.

The -> operator works the same for pointers to class objects as it did when you were dealing with a struct. Here, using the pointer this demonstrates that it exists and does work, but it’s quite unnecessary to use it explicitly in this case. If you change the return statement in the Compare() function to be

```
return Volume() > xBox.Volume();
```

you’ll find that the program works just as well. Any references to unadorned member names are automatically assumed to be the members of the object pointed to by this.

## Chapter 7

You use the Compare() function in main() to check the relationship between the volumes of the objects match and cigar. The output from the program is:

```
Constructor called.
Constructor called.
match is smaller than cigar
```

This confirms that the cigar object is larger than the match object.

It also wasn’t essential to define the Compare() function as a class member. You could just as well have written it as an ordinary function with the objects as arguments. Note that this isn’t true of the function Volume(), because it needs to access the private data members of the class. Of course, if you implemented the Compare() function as an ordinary function, it wouldn’t have access to the pointer this, but it would still be very simple:

```
// Comparing two CBox objects - ordinary function version
int Compare(CBox B1, CBox B2)
{
    return B1.Volume() > B2.Volume();
}
```

This has both objects as arguments and returns true if the volume of the first is greater than the last. You would use this function to perform the same function as in the last example with this statement:

```
if(Compare(cigar, match))
    cout << endl
        << "match is smaller than cigar";
else
    cout << endl
        << "match is equal to or larger than cigar";
```

If anything, this looks slightly better and easier to read than the original version; however, there’s a much better way to do this, which you will learn about in the next chapter.

## const Objects of a Class

The Volume() function that you defined for the CBox class does not alter the object for which it is called, neither does a function such as getHeight() that returns the value of the m_Height member. Likewise, the Compare() function in the previous example didn’t change the class objects at all. This may seem at first sight to be a mildly interesting but largely irrelevant observation, but it isn’t, it’s quite important. Let’s think about it.

You will undoubtedly want to create class objects that are fixed from time to time, just like values such as pi or inchesPerFoot that you might declare as const double. Suppose you wanted to define a CBox object as const(because it was a very important standard sized box, for instance. You might define it with the following statement:

```
const CBox standard(3.0, 5.0, 8.0);
```
