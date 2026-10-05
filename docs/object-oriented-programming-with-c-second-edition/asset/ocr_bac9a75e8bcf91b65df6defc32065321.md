# Constructors and Destructors 111

```
/*End of A.cpp*/
/*Beginning of AMain.cpp*/
#include<A.h>
#include<iostream.h>
void main()
{
    A A1;
    cout="End of program\n";
}
/*End of AMain.cpp*/
```

# Output

Constructor of class A called
End of program
Destructor of class A called

We can see, the name of the destructor is the same as the name of the class prefixed with a tilde sign. Moreover, the destructor does not return anything. The compiler defines the destructor in order to resolve the call to the destructor that it compulsorily places for the object going out of scope.

Destructors do not take any arguments. Therefore, they cannot be overloaded.
Why should we define our own destructor? We must remember that the destructor is also a member function. It is called for objects. Therefore, it can access the data members of the object for which it has been called.

Let us think of a relevant definition for the destructor of the class Distance. What would we like to do for us? What should it do to the data members of the object that is going out of scope? Should we set them to zero?

```
Distance::~Distance()
{
    iFeet=0;
    iches=0.0;
}
```

But what is the use? The destructor is anyway going out of scope immediately after the destructor executes.

But we must define the destructor for classes whose objects, during their lifetime, acquire resources that are outside the objects themselves. Let us take the example of the class String. We consider the following code block.

```
{
    .
    .
    .
    String s1("abc");
    .
    .
    .
}
```

The memory was allocated to 's1' itself gets deallocated when this block finishes execution. But 's1.cStr' was pointing at a memory block that was dynamically allocated in the heap area. This memory block was outside the memory block occupied by 's1' itself. After 's1' gets destroyed, this memory block remains allocated as a locked up resource. The only pointer that pointing at ('s1.cStr') is no longer available. This is a memory leak. It should be prevented. We should deallocate the memory block at which the pointer any