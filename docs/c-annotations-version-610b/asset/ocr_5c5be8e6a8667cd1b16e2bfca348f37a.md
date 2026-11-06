```
~~~cpp
one = two;                    ERROR: not available
one = factory();              Mov::operator=(  tmp.d_x
                                  Mov &&tmp)
}
~~~
```

To reestablish the defaults, append `= default` to the appropriate declarations:

```
~~~cpp
class Defaults
{
    int d_x;
    Mov d_mov;

public:
    Defaults()                    = default;
    Defaults(Defaults &&tmp)      = default;
    Defaults(int x);
    // Default(Default const &) remains available

    Defaults operator=(Defaults const &rhs) = default;
    Defaults operator=(Defaults &&tmp);
};
~~~
```

Be cautious, declaring defaults, as default implementations copy data members of primitive types byte-by-byte from the source object to the destination object. This is likely to cause problems with pointer type data members.

The `= default` suffix can only be used when declaring constructors or assignment operators in the class's public section.

# ### 9.7.8 Moving: implications for class design (C++11)

Here are some general rules to apply when designing classes offering value semantics (i.e., classes whose objects can be used to initialize other objects of their class and that can be assigned to other objects of their class):

+   - Classes using pointers to dynamically allocated memory, owned by the class's objects must be provided with a copy constructor, an overloaded copy assignment operator and a destructor;

+   - Classes using pointers to dynamically allocated memory, owned by the class's objects, should be provided with a move constructor and a move assignment operator;

+   - Classes using composition may benefit from move constructors and move assignment operators as well. Some classes support neither move nor copy construction and assignment (for example: stream classes don't). If your class contains data members of such class types then defining move operations is pointless.

In the previous sections we've also encountered an important design principle that can be applied to move-aware classes:

> > *Whenever a member of a class receives a const & to an object of its own class and creates a copy of that object to perform its actual actions on, then that function's implementation can be implemented by an overloaded function expecting an rvalue reference.*

The former function can now call the latter by passing `std::move(tmp)` to it. The advantages of this design principle should be clear: there is only one implementation of the actual actions, and the class automatically becomes *move-aware* with respect to the involved function.