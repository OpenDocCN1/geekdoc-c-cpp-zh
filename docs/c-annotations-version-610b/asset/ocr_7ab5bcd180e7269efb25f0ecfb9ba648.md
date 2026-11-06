```
```cpp
{
    public:
        std::string const &name()    const;
        std::string const &address()  const;
        std::string const &phone()    const;
        size_t mass()                 const;
};
```
```

The rule of thumb given in section 3.1.3 applies here too: whichever appears to the left of the keyword `const`, is not altered. With member functions this should be interpreted as ‘doesn’t alter its own data’.

When implementing a const member function the const attribute must be repeated:

```
```cpp
string const &Person::name() const
{
    return d_name;
}
```
```

The compiler prevents the data members of a class from being modified by one of its const member functions. Therefore a statement like

```
```cpp
d_name[0] = toupper(static_cast<unsigned char>(d_name[0]));
```
```

results in a compiler error when added to the above function’s definition.

Const member functions are used to prevent inadvertent data modification. Except for constructors and the destructor (cf. chapter 9) only const member functions can be used with (plain, references or pointers to) const objects.

Const objects are frequently encountered as `const &` parameters of functions. Inside such functions only the object’s const members may be used. Here is an example:

```
```cpp
void displayMass(ostream &out, Person const &person)
{
    out << person.name() << " weighs " << person.mass() << " kg.\n";
}
```
```

Since person is defined as a Person const & the function displayMass cannot call, e.g., `person.setMass(75)`.

The const member function attribute can be used to overload member functions. When functions are overloaded by their const attribute the compiler uses the member function matching most closely the const-qualification of the object:

+   - When the object is a `const` object, only const member functions can be used.
+   - When the object is not a `const` object, non-const member functions are used, unless only a const member function is available. In that case, the const member function is used.

The next example illustrates how (non) const member functions are selected:

```
```cpp
#include <iostream>
using namespace std;

class Members
{
    public:
```
```