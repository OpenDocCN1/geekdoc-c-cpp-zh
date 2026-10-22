```
D d2; // X(int, int, int) called by D()
```

In this example, the problem occurs because the implicitly generated default constructor of class D is different in the two translation units. One calls the X constructor taking two arguments, and the other calls the X constructor taking three arguments. If anything, this example is an additional incentive to limit default arguments to one location in the program (if possible, this location should be in a header file). Fortunately, placing default arguments on out-of-class definitions is a rare practice.

There is also an exception to the rule that says that identical tokens must refer to identical entities. If identical tokens refer to unrelated constants that have the same value and the address of the resulting expressions is not used (not even implicitly by binding a reference to a variable producing the constant), then the tokens are considered equivalent. This exception allows for program structures like the following:

```
```cpp
// == header.hpp:
#ifndef HEADER_HPP
#define HEADER_HPP

int const length = 10;

class MiniBuffer {
char buf[length];
...
};

#endif // HEADER_HPP
```
```

In principle, when this header file is included in two different translation units, two distinct constant variables named `length` are created because `const` in this context implies `static`. However, such constant variables are often meant to define compile-time constant values, not a particular storage location at run time. Hence, if we don’t force such a storage location to exist (by referring to the address of the variable), it is sufficient for the two constants to have the same value.

Finally, a note about templates. The names in templates bind in two phases. *Nondependent names* bind at the point where the template is defined. For these, the equivalence rules are handled similarly to other nontemplate definitions. For names that bind at the point of instantiation, the equivalence rules must be applied at that point, and the bindings must be equivalent.