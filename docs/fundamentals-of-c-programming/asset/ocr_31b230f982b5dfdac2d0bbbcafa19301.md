This code generates a pseudorandom number at run time. If it generates an even number, it directs p to point to a plain Text object; otherwise, it directs p to a FancyText object. Which method will this code call, Text::get or FancyText::get? Since the code generates the pseudorandom number at run time, the compiler is powerless to determine the exact type of the object to which p points; thus, the compiler cannot determine which get method to call. The compiler can, however, generate code that jumps to the method found at the address stored in p's associated vtable at the index corresponding to the get method.

Listing 17.9 (vtablesize.cpp) demonstrates that the vtable pointer does occupy space within an object that contains a virtual method.

```
#include <iostream>

// A class with no virtual methods
class NoVTable {
 int data;
 public:
 void set(int d) { data = d; }
 int get() { return data; }
};

// A class with virtual methods
class HasVTable {
 int data;
 public:
 virtual void set(int d) { data = d; }
 virtual int get() { return data; }
};

int main() {
 NoVTable no_vtable;
 HasVTable has_vtable;
 no_vtable.set(10);
 has_vtable.set(10);
 std::cout << "no_vtable size = " << sizeof no_vtable << '\n';
 std::cout << "has_vtable size = " << sizeof has_vtable << '\n';
}
```

The output of Listing 17.9 (vtablesize.cpp) is

```
no_vtable size = 4
has_vtable size = 8
```

A NoVTable object requires four bytes for its integer field, but a HasVTable object occupies eight bytes—four bytes for its integer field and four bytes for its secret vtable pointer.

Dynamic binding enables a powerful technique in object-oriented programming called polymorphism. A polymorphic method behaves differently depending on the actual type of object upon which it is invoked. Consider Listing 17.10 (polymorphicvector.cpp).

```
#include <string>
```