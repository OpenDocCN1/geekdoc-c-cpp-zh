
```cpp
private:
    enum {Lbs_per_stn = 14};      // pounds per stone
    int stone;                    // whole stones
    double pds_left;              // fractional pounds
    double pounds;                // entire weight in pounds
public:
    Stonewt(double lbs);          // construct from double pounds
    Stonewt(int stn, double lbs); // construct from stone, lbs
    Stonewt();                    // default constructor
    ~Stonewt();
    void show_lbs() const;        // show weight in pounds format
    void show_stn() const;        // show weight in stone format
    // conversion functions
    operator int() const;
    operator double() const;
};
#endif
```

Listing 11.20 shows Listing 11.18 modified to include the definitions for these two conversion functions. Note that each function returns the desired value, even though there is no declared return type. Also note that the int conversion definition rounds to the nearest integer rather than truncating. For example, if pounds is 114.4, then pounds + 0.5 is 114.9, and int (114.9) is 114. But if pounds is 114.6, pounds + 0.5 is 115.1, and int (115.1) is 115.

### Listing 11.20 stonewt1.cpp

```cpp
// stonewt1.cpp -- Stonewt class methods + conversion functions
#include <iostream>
using std::cout;
#include "stonewt1.h"

// construct Stonewt object from double value
Stonewt::Stonewt(double lbs)
{
    stone = int (lbs) / Lbs_per_stn;    // integer division
    pds_left = int (lbs) % Lbs_per_stn + lbs - int(lbs);
    pounds = lbs;
}

// construct Stonewt object from stone, double values
Stonewt::Stonewt(int stn, double lbs)
{
    stone = stn;
    pds_left = lbs;
    pounds = stn * Lbs_per_stn + lbs;
}

Stonewt::Stonewt()          // default constructor, wt = 0
{
    stone = pounds = pds_left = 0;
}

Stonewt::~Stonewt()         // destructor
{
}

// show weight in stones
void Stonewt::show_stn() const
{
    cout << stone << " stone, " << pds_left << " pounds\n";
}

// show weight in pounds
void Stonewt::show_lbs() const
{
    cout << pounds << " pounds\n";
}

// conversion functions
Stonewt::operator int() const
{
    return int (pounds + 0.5);
}

Stonewt::operator double() const
{
    return pounds;
}
```

Listing 11.21 tests the new conversion functions. The assignment statement in the program uses an implicit conversion, whereas the final `cout` statement uses an explicit type cast. Be sure to compile Listing 11.20 along with Listing 11.21.

### Listing 11.21 **stone1.cpp**

```cpp
// stone1.cpp -- user-defined conversion functions
// compile with stonewt1.cpp
#include <iostream>
#include "stonewt1.h"

int main()
{
    using std::cout;
    Stonewt poppins(9,2.8);    // 9 stone, 2.8 pounds
    double p_wt = poppins;      // implicit conversion
    cout << "Convert to double => ";
    cout << "Poppins: " << p_wt << " pounds.\n";
    cout << "Convert to int => ";
    cout << "Poppins: " << int (poppins) << " pounds.\n";
    return 0;
}
```

Here’s the output from the program in Listings 11.19, 11.20, and 11.21, which shows the result of converting the type Stonewt object to type double and to type int:

```text
Convert to double => Poppins: 128.8 pounds.
Convert to int => Poppins: 129 pounds.
```

## Applying Type Conversions Automatically

Listing 11.21 uses int (poppins) with cout. Suppose that, instead, it omitted the explicit type cast:

```cpp
cout << "Poppins: " << poppins << " pounds.\n";
```

Would the program use an implicit conversion, as in the following statement?

```cpp
double p_wt = poppins;
```

The answer is no. In the p_wt example, the context indicates that poppins should be converted to type double. But in the cout example, nothing indicates whether the conversion should be to int or to double. Facing this lack of information, the compiler would complain that you were using an ambiguous conversion. Nothing in the statement indicates what type to use.

Interestingly, if the class defined only the double conversion function, the compiler would accept the statement. That’s because with only one conversion possible, there is no ambiguity.

You can have a similar situation with assignment. With the current class declarations, the compiler rejects the following statement as being ambiguous:

```cpp
long gone = poppins;    // ambiguous
```

In C++, you can assign both int and double values to a long variable, so the compiler legitimately can use either conversion function. The compiler doesn’t want the responsibility of choosing which. But if you eliminate one of the two conversion functions, the compiler accepts the statement. For example, suppose you omit the double definition. Then the compiler will use the int conversion to convert poppins to a type int value. Then it converts the int value to type long when assigning it to gone.

When the class defines two or more conversions, you can still use an explicit type cast to indicate which conversion function to use. You can use either of these type cast notations:

```cpp
long gone = (double) poppins;  // use double conversion
long gone = int (poppins);     // use int conversion
```

The first of these statements converts poppins weight to a double value, and then assignment converts the double value to type long. Similarly, the second statement converts poppins first to type int and then to long.

Like conversion constructors, conversion functions can be a mixed blessing. The problem with providing functions that make automatic, implicit conversions is that they may make conversions when you don’t expect them. Suppose, for example, that you happen to write the following code when you’re sleep deprived:

```cpp
int ar[20];
...
Stonewt temp(14, 4);
...
int Temp = 1;
...
cout << ar[temp] << "!\n";  // used temp instead of Temp
```

Normally, you’d expect the compiler to catch a blunder such as using an object instead of an integer as an array index. But the Stonewt class defines an operator int(), so the Stonewt object temp is converted to the int 200 and be used as an array index. The moral is that often it’s best to use explicit conversions and exclude the possibility of implicit conversions. In C++98, the keyword explicit doesn’t work with conversion functions, but C++11 removes that limitation. So with C++11, you can declare a conversion operator as explicit:

```cpp
class Stonewt
{
...
// conversion functions
    explicit operator int() const;
    explicit operator double() const;
};
```

With these declarations in place, you would use a type cast to invoke the operators. Another approach is to replace a conversion function with a nonconversion function that does the same task—but only if called explicitly. That is, you can replace

```cpp
Stonewt::operator int() { return int (pounds + 0.5); }
```

with

```cpp
int Stonewt::Stone_to_Int() { return int (pounds + 0.5); }
```

This disallows the following:

```cpp
int plb = poppins;
```

But if you really need a conversion, it allows the following:

```cpp
int plb = poppins.Stone_to_Int();
```

> **Caution**
>
> You should use implicit conversion functions with care. Often a function that can only be invoked explicitly is the best choice.

In summary, then, C++ provides the following type conversions for classes:

- A class constructor that has but a single argument serves as an instruction for converting a value of the argument type to the class type. For example, the Stonewt class constructor with a type int argument is invoked automatically when you assign a type int value to a Stonewt object. However, using `explicit` in the constructor declaration eliminates implicit conversions and allows only explicit conversions.
- A special class member operator function called a *conversion function* serves as an instruction for converting a class object to some other type. The conversion function is a class member, has no declared return type, has no arguments, and is called operator `typeName()`, where `typeName` is the type to which the object is to be converted. This conversion function is invoked automatically when you assign a class object to a variable of that type or use the type cast operator to that type.

## Conversions and Friends

Let’s bring addition to the Stonewt class. As mentioned in the discussion of the Time class, you can use either a member function or a friend function to overload addition. (To simplify matters, assume that no conversion functions of the operator double() form are defined.) You can implement addition with the following member function:

```cpp
Stonewt Stonewt::operator+(const Stonewt & st) const
{
    double pds = pounds + st.pounds;
    Stonewt sum(pds);
    return sum;
}
```

Or you can implement addition as a friend function this way:

```cpp
Stonewt operator+(const Stonewt & st1, const Stonewt & st2)
{
    double pds = st1.pounds + st2.pounds;
    Stonewt sum(pds);
    return sum;
}
```

Remember, you can provide the method definition or the friend definition but not both. Either form lets you do the following:
