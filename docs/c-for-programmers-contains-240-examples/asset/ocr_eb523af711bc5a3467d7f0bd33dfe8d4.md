```
```cpp
// Fig. 10.25: Interface.h
// Proxy Class Interface definition.
// Client sees this source code, but the source code does not reveal
// the data layout of class Implementation.

class Implementation; // forward class declaration required by line 17

class Interface
{
public:
   Interface( int ); // constructor
   void setValue( int ); // same public interface as
   int getValue() const; // class Implementation has
   ~Interface(); // destructor
private:
   // requires previous forward declaration (line 6)
   Implementation *ptr;
}; // end class Interface
```
```

Using a pointer in this manner allows us to hide the implementation details of class `Implementation` from the client. Notice that the only mentions in class `Interface` of the proprietary `Implementation` class are in the pointer declaration (line 17) and in line 6, a *forward class declaration*. When a class definition (such as class `Interface`) uses only a pointer or reference to an object of another class (such as to an object of class `Implementation`), the class header file for that other class (which would ordinarily reveal the private data of that class) is not required to be included with `#include`. This is because the compiler doesn’t need to reserve space for an object of the class. The compiler does need to reserve space for the pointer or reference. The sizes of pointers and references are characteristics of the hardware platform on which the compiler runs, so the compiler already knows those sizes. You can simply declare that other class as a data type with a forward class declaration (line 6) before the type is used in the file.

The member-function implementation file for proxy class `Interface` (Fig. 10.26) is the only file that includes the header file `Implementation.h` (line 5) containing class `Implementation`. The file `Interface.cpp` (Fig. 10.26) is provided to the client as a pre-compiled object code file along with the header file `Interface.h` that includes the function prototypes of the services provided by the proxy class. Because file `Interface.cpp` is made available to the client only as object code, the client is not able to see the interactions between the proxy class and the proprietary class (lines 9, 17, 23 and 29). Notice that the proxy class imposes an extra “layer” of function calls as the “price to pay” for hiding the private data of class `Implementation`. Given the speed of today’s computers and the fact that many compilers can inline simple function calls automatically, the effect of these extra function calls on performance is often negligible.

Figure 10.27 tests class `Interface`. Notice that only the header file for `Interface` is included in the client code (line 7)—there is no mention of the existence of a separate class called `Implementation`. Thus, the client never sees the private data of class `Implementation`, nor can the client code become dependent on the `Implementation` code.