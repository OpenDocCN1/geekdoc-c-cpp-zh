a person, this data can be read by the functions defined on lines [30, 36]. These are accessed by calling the internal `fData` member.

We have come a long way from trying to use a simple int or long to store the PESEL ID, all the way to the efficient `PESEL` class that correctly represents the ID in any system, offers additional functionality, and hides the implementation details at the same time. We are interested in measuring the total size of the PESEL object, which is done by the following code:

```
```cpp
#include "Embedded_PESEL.h"
void Embedded_PESEL_Test (void )
{
    std::cout << "Size with wrapped object: " << sizeof( PESEL ) << std::endl;
}
```
```

The output is

```
```text
Size with wrapped object: 6
```
```

# 4.15.4.2 Inherited *PESEL*

In this section, we consider the properties of the second solution, shown in Figure 4.23b. In this case, the `PESEL` class is derived from `TLongNumberFor< 11 >`, so we can say that PESEL “is” a kind of `TLongNumberFor`. To allow inheritance, the `ALLOW_INHERITANCE` flag needs to be set to 1, as is done on line [1]. Then, as previously, on line [2], the `LongNumber.h` header is included.

The definition of the PESEL class, derived from `TLongNumberFor< 11 >`, starts on line [7] of Listing 4.36. The rest is almost identical to in the definition shown in Listing 4.35, except for the additional virtual destructor defined on line [28]. This is usually necessary for the correct deletion of inherited classes, as discussed in Section 4.11. Also, there is no `fData` member, since all data is stored in the base class. Therefore, the `GetYearOfBirth` (line [32]) and `GetSex` (line [38]) members can directly call the `GetNumberAt` member from the base class. For this purpose, on line [12], `GetNumberAt` is inserted into the scope of the PESEL class with the `using` directive.

# **Listing 4.36** Definition of the PESEL class derived from `TLongNumberFor< 11 >` (in *LongNumber,Derived_PESEL.h*).

```
```cpp
#define ALLOW_INHERITANCE 1
#include "LongNumberFor.h"


///////////////////////////////////////////////
// The "is-a" version
class PESEL : public TLongNumberFor< 11 >
{
public:

    using BaseClass = TLongNumberFor< 11 >;
    using BaseClass::GetNumberAt;

private:

    // Some constants specific to the Polish PESEL number
    enum { kBirthYear_Dec = 10, kBirthYear_Sngl = 9, kSex = 1 };
```
```