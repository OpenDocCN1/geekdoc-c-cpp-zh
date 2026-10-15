```
#include <new> // standard operator new and set_new_handler
using std::set_new_handler;

#include <cstdlib> // abort function prototype
using std::abort;

// handle memory allocation failure
void customNewHandler()
{
    cerr << "customNewHandler was called";
    abort();
} // end function customNewHandler

// using set_new_handler to handle failed memory allocation
int main()
{
    double *ptr[ 50 ];

    // specify that customNewHandler should be called on
    // memory allocation failure
    set_new_handler( customNewHandler );

    // aim each ptr[i] at a big block of memory; customNewHandler will be
    // called on failed memory allocation
    for ( int i = 0; i < 50; i++ )
    {
        ptr[ i ] = new double[ 50000000 ]; // may throw exception
        cout << "ptr[" << i << "] points to 50,000,000 new doubles\n";
    } // end for

    return 0;
} // end main
```

```
ptr[0] points to 50,000,000 new doubles
ptr[1] points to 50,000,000 new doubles
ptr[2] points to 50,000,000 new doubles
customNewHandler was called
```

Fig. 16.7 | set_new_handler specifying the function to call when new fails. (Part 2 of 2.)

# 16.12 Class auto_ptr and Dynamic Memory Allocation

A common programming practice is to allocate dynamic memory, assign the address of that memory to a pointer, use the pointer to manipulate the memory and deallocate the memory with delete when the memory is no longer needed. If an exception occurs after successful memory allocation but before the delete statement executes, a memory leak could occur. The C++ standard provides class template auto_ptr in header file <memory> to deal with this situation.

An object of class auto_ptr maintains a pointer to dynamically allocated memory. When an auto_ptr object destructor is called (for example, when an auto_ptr object goes out of scope), it performs a delete operation on its pointer data member. Class template auto_ptr provides overloaded operators * and -> so that an auto_ptr object can be used