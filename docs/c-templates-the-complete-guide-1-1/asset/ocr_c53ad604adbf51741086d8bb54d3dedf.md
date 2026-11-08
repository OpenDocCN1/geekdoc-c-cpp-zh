```
```cpp
class Empty {
    using Int = int; // type alias members don't make a class nonempty
};

class EmptyToo : public Empty {
};

class EmptyThree : public EmptyToo {
};

int main()
{
    std::cout << sizeof(Empty) << " " << sizeof(EmptyToo)
              << " " << sizeof(EmptyThree);
}
```
```

If your compiler implements the EBCO, it will print the same size for every class, but none of these classes has size zero (see Figure 22.1). This means that within class EmptyToo, the class Empty is not given any space. Notice also that an empty class with nonvirtual empty bases (and no other bases) is also empty. This explains why class EmptyThree can also have the same size as EmptyToo. If your compiler does not implement the EBCO, it will print different sizes (see Figure 22.2).

Click here to view code image

*Figure 22.1. Layout of EmptyThree by a compiler that implements the EBCO.*

Click here to view code image

*Figure 22.2. Layout of EmptyThree by a compiler that does not implement the EBCO.*

Consider an example that runs into a constraint of the EBCO:

Click here to view code image

`inherit/ebco2.cpp`

```
```cpp
#include <iostream>

class Empty {
    using Int = int; // type alias members don't make a class nonempty
};

class EmptyToo : public Empty {
};

class NonEmpty : public Empty, public EmptyToo {
};

int main()
{
    std::cout << sizeof(Empty) << " " << sizeof(EmptyToo)
              << " " << sizeof(NonEmpty);
}
```
```

In this case as a surprise that class NonEmpty is not an empty class. After all, it does not have any members and neither do its base classes. However, the base classes Empty and EmptyToo of NonEmpty cannot be allocated to the same address because they would then have the same address. To avoid this, the compiler offsets the base class Empty subobject of NonEmpty. In other words, two subobjects of the same type cannot have the same address.