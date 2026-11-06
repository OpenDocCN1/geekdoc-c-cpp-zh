```
```
{
                                        // initialization
    size_t (PointerDemo::*getPtr)() const = &PointerDemo::get;
    size_t PointerDemo::*valuePtr       = &PointerDemo::d_value;

    getPtr    = &PointerDemo::get;          // assignment
    valuePtr  = &PointerDemo::d_value;
}
```
```

This involves nothing special. The difference with pointers at global scope is that we're now restricting ourselves to the scope of the PointerDemo class. Because of this restriction, all pointer definitions and all variables whose addresses are used must be given the PointerDemo class scope.

Pointers to members can also be used with virtual member functions. No special syntax is required when pointing to virtual members. Pointer construction, initialization and assignment is done identically to the way it is done with non-virtual members.

# ## 16.3 Using pointers to members

Using pointers to members to call a member function requires the existence of an object of the class of the members to which the pointer to member refers to. With pointers operating at global scope, the dereferencing operator * is used. With pointers to objects the field selector operator operating on pointers (->) or the field selector operating on objects (.) can be used to select appropriate members.

To use a pointer to member in combination with an object the pointer to member field selector ( .* ) must be specified. To use a pointer to a member via a pointer to an object the 'pointer to member field selector through a pointer to an object' (->*) must be specified. These two operators combine the notions of a field selection (the . and -> parts) to reach the appropriate field in an object and of dereferencing: a dereference operation is used to reach the function or variable the pointer to member points to.

Using the example from the previous section, let's see how we can use pointers to member functions and pointers to data members:

```
```
#include <iostream>

class PointerDemo
{
    public:
        size_t d_value;
        size_t get() const;
};

inline size_t PointerDemo::get() const
{
    return d_value;
}

using namespace std;

int main()
{
    size_t (PointerDemo::*getPtr)() const = &PointerDemo::get;          // initialization
    size_t PointerDemo::*valuePtr       = &PointerDemo::d_value;

    PointerDemo object;                                      // (1) (see text)
    PointerDemo *ptr = &object;
```
```