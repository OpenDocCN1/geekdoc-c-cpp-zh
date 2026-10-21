
(~). The class destructor doesn’t return a value and doesn’t have parameters defined. For the CBox class, the prototype of the class destructor is:

```
~CBox();    // Class destructor prototype
```

Because a destructor has no parameters, there can only ever be one destructor in a class.

> It’s an error to specify a return value or parameters for a destructor.

## The Default Destructor

All the objects that you have been using up to now have been destroyed automatically by the default destructor for the class. The default destructor is always generated automatically by the compiler if you do not define your own class destructor. The default destructor doesn’t delete objects or object members that have been allocated in the free store by the operator new. If space for class members has been allocated dynamically in a contructor, you must define your own destructor that explicitly use the delete operator to release the memory that has been allocated by the constructor using the operator new, just as you would with ordinary variables. You need some practice in writing destructors, so let’s try it out.

## Try It Out ... A Simple Destructor

To get an appreciation of when the destructor for a class is called, you can include a destructor in the class CBox. Here’s the definition of the example including the CBox class with a destructor:

```
// Ex8_01.cpp
// Class with an explicit destructor
#include <iostream>
using std::cout;
using std::endl;

class CBox                 // Class definition at global scope
{
public:
    // Destructor definition
    ~CBox()
    {
        cout << "Destructor called." << endl;
    }

    // Constructor definition
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0);
        m_Length(lv), m_Width(wv), m_Height(hv)
    {
        cout << endl << "Constructor called.";
    }

    // Function to calculate the volume of a box
    double Volume() const
    {
        return m_Length*m_Width*m_Height;
    }

    // Function to compare two boxes which returns true
```
// if the first is greater that the second, and false otherwise
int compare(CBox* pBox) const
{
    return this->Volume() > pBox->Volume();
}

private:
    double m_Length;      // Length of a box in inches
    double m_Width;       // Width of a box in inches
    double m_Height;      // Height of a box in inches
};

// Function to demonstrate the CBox class destructor in action
int main()
{
    CBox boxes[5];        // Array of CBox objects declared
    CBox cigar(8.0, 5.0, 1.0);  // Declare cigar box
    CBox match(2.2, 1.1, 0.5);  // Declare match box
    CBox* pB1 = &cigar;         // Initialize pointer to cigar object address
    CBox* pB2 = 0;              // Pointer to CBox initialized to null

    cout << endl
         << "Volume of cigar is "
         << pB1->Volume();      // Volume of obj. pointed to

    pB2 = boxes;                // Set to address of array
    boxes[2] = match;           // Set 3rd element to match
    cout << endl
         << "Volume of boxes[2] is "
         << (pB2 + 2)->Volume();  // Now access thru pointer

    cout << endl;
    return 0;
}
```

## How It Works

The only thing that the CBox class destructor does is to display a message showing that it was called.

The output is:

```
Constructor called.
Constructor called.
Constructor called.
Constructor called.
Constructor called.
Constructor called.
Constructor called.
Volume of cigar is 40
Volume of boxes[2] is 1.21
Destructor called.
Destructor called.
Destructor called.
Destructor called.
Destructor called.
Destructor called.
Destructor called.
```

You get one call of the destructor at the end of the program for each of the objects that exist. For each constructor call that occurred, there’s a matching destructor call. You don’t need to call the destructor explicitly here. When an object of a class goes out of scope, the compiler arranges for the destructor for the class to be called automatically. In our example, the destructor calls occur after main() has finished executing, so it’s quite possible for an error in a destructor to cause a program to crash after main() has safely terminated.

## Destructors and Dynamic Memory Allocation

You will find that you often want to allocate memory for class data members dynamically. You can use the operator new in a constructor to allocate space for an object member. In such a case, you must assume responsibility for releasing the space when the object is no longer required by providing a suitable destructor. Let’s first define a simple class where we can do this.

Suppose you want to define a class where each object is a message of some description, for example, a text string. The class should be as memory efficient as possible so, rather than defining a data member as a char array big enough to hold the maximum length string that you might require, you’ll allocate memory in the free store for the message when an object is created. Here’s the class definition:

```
//Listing 08_01
class CMessage
{
private:
    char* pmessage;                // Pointer to object text string

public:
    // Function to display a message
    void ShowIt() const
    {
        cout << endl << pmessage;
    }

    // Constructor definition
    CMessage(const char* text = "Default message")
    {
        pmessage = new char[strlen(text) + 1];   // Allocate space for text
        strcpy(pmessage, text);                  // Copy text to new memory
    }

    ~CMessage();                           // Destructor prototype
};
```

This class has only one data member defined, pmessage, which is a pointer to a text string. This is defined in the private section of the class, so that it can’t be accessed from outside the class.

In the public section, you have the ShowIt() function that outputs a CMessage object to the screen. You also have the definition of a constructor and you have the prototype for the class destructor, ~CMessage(), which I’ll come to in a moment.

The constructor for the class requires a string as an argument, but if none is passed, it uses the default string that is specified for the parameter. The constructor obtains the length of the string supplied as the argument, excluding the terminating NULL, by using the library function strlen(). For the constructor to use this library function, there must be a #include statement for the <cstring> header file. The constructor determines the number of bytes of memory necessary to store the string in the free store by adding 1 to the value that the function strlen() returns.

> Of course, if the memory allocation fails, an exception will be thrown that will terminate the program. If you want to manage such a failure to provide a more graceful end to the program, you would catch the exception within the constructor code. (See Chapter 6 for information on handling out-of-memory conditions.)

Having obtained the memory for the string using the operator new, you use the strcpy() library function that is also declared in the <cstring> header file to copy the string supplied as the argument to the constructor into the memory allocated for it. The strcpy() function copies the string specified by the second pointer argument to the address contained in the first pointer argument.

You now need to write a class destructor that frees up the memory allocated for a message. If you don’t provide a destructor for the class, there’s no way to delete the memory allocated for an object. If you use this class as it stands in a program where a large number of CMessage objects are created, the free store is gradually eaten away until the program fails. It’s easy for this to occur in circumstances where it may not be obvious that it is happening. For example, if you create a temporary CMessage object in a function that is called many times in a program, you might assume that the objects are being destroyed at the return from the function. You’d be right about that, of course, but the free store memory is released. Thus for each call of the function, more of the free store is occupied by memory for discarded CMessage objects.

The code for the CMessage class destructor is as follows:

```
// Listing 08_02
// Destructor to free memory allocated by new
CMessage::~CMessage()
{
    cout << "Destructor called."        // Just to track what happens
         << endl;
    delete[] pmessage;                // Free memory assigned to pointer
}
```

Because you’re defining the destructor outside of the class definition, you must qualify the name of the destructor with the class name, CMessage. All the destructor does is display a message so that you can see what’s going on and then use the delete operator to free the memory pointed to by the member pmessage. Note that you have to include the square brackets with delete because you’re deleting an array (of type char).

## Try It Out     Using the Message Class

You can exercise the CMessage class with a little example:

```
// Ex8_02.cpp
// Using a destructor to free memory
#include <iostream>        // For stream I/O
```
