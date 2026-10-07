
# Automatic Conversions and Type Casts for Classes 613

Conversion functions are user-defined type casts, and you can use them the way you would use a type cast. For example, if you define a Stonew-to-double conversion function, you can use the following conversions:

```
Stonew(285.7);
double host = double(wolfe); // syntax #1
double thinker = (double) wolfe; // syntax #2
```

Or you can let the compiler figure out to:
Stonew wells(20,3);
double star = wells; // implicit use of conversion function

The compiler, noting that the right side is type Stonew and the left side is type double, looks to see if you have a defined conversion function that matches this description. (If it can't find such a definition, the compiler generates an error message to the effect that it can't assign a Stonew to a double.)

So do you create a conversion function? To convert type typeName, you use a conversion function in this form:
operator typeName();

Note the following points:

- The conversion function must be a class method.
- The conversion function must not specify a return type.
- The conversion function must have no arguments.

For example, a function to convert type double would have this prototype:
operator double();

The typeName part (in this typeName is double) tells the conversion type to convert to, so no return type is needed. The fact that a class method has it to be invoked by a particular class object, and tells that the function which value to convert. Thus, the function doesn't need arguments.

To add functions that convert stone_wt objects to int and to type double, requires adding the following prototypes to the class declaration:

```
operator int();
operator double();
```

Listing 11.19 shows the modified class declaration.

# Listing 11.19 stonew1.h

```
// stonew1.h revised definition for the Stonew class
#ifndef STONEWT1_H_
#define STONEWT1_H_
class Stonew
{

private:

```
enum (Lbs_per_stn = 14);      // pounds per stone
int stone;                               // whole stones
double pds_left;                         // fractional pounds
double pounds;                           // entire weight in pounds
public:
Stonew(double lbs);                    // construct from double pounds
Stonew(int stn, double lbs);           // construct from stone, lbs
Stonew();                                // default constructor
~Stonew();
void show_lbs(const) const;               // show weight in pounds format
void show_stn(const) const;               // show weight in stone format
```

// conversion functions
operator int() const;
operator double() const;

};
#endif
```

Listing 11.20 shows 11.18 modified to include the definitions for these two conversion functions. Note that each function returns the desired value, even though there is no declared return type. Also note that the int conversion rounds to the nearest integer rather than truncating. For example, if pounds is 114.4, then pounds + 0.5 is 114.9, and int (114.9) is 114. But if pounds is 114.6, pounds + 0.5 is 115.1, and int (115.1) is 115.

# Listing 11.20 stonew1.cpp

```
// stonew1.cpp -- Stonew class methods + conversion functions
#include <iostream>
using std::cout;
#include "stonew1.h"

// construct Stonew object from double value
Stonew::Stonew(double lbs)
{
    stone = int(lbs) / Lbs_per_stn;      // integer division
    pds_left = int(lbs) % Lbs_per_stn + lbs;
}

// construct Stonew object from stone, double values
Stonew::Stonew(int stn, double lbs)
{
    stone = stn;
    pds_left = lbs;
    pounds = stn * Lbs_per_stn + lbs;
}

# Automatic Conversions and Type Casts for Classes

```
Stonew::Stonew() // default constructor, wt = 0
{
    stone = pounds = pds_left = 0;
}

Stonew::~Stonew() // destructor
{
}

// show weight in stones
void Stonew::show_stn() const
{
    cout << stone << " stone," << pds_left << " pounds\n";
}

// show weight in pounds
void Stonew::show_lbs() const
{
    cout << pounds << " pounds\n";
}

// conversion functions
operator int() const
{
    return int(pounds + 0.5);
}

operator double() const
{
    return pounds;
}
```
```

Listing 11.21 tests the new conversion functions. The assignment statement in the program uses an implicit conversion, whereas the final cout statement uses an explicit type cast. Be sure to compile Listing 11.20 along with Listing 11.21.

# Listing 11.21 stonew.cpp

```
// stonew.cpp -- user-defined conversion functions
// compile with stonew1.cpp
#include <iostream>
#include "stonew1.h"

int main()
{
using std::cout;
Stonew poppins(9,2.8); // 9 stone, 2.8 pounds
double p_wt = poppins; // implicit conversion
cout << "Convert to double =>";
cout << "Poppins: " << p_wt << " pounds\n"
cout << "Convert to int =>";
cout << "Poppins: " << int(poppins) << " pounds\n"
return 0;
}
```

Here’s the output from the program in Listings 11.19, 11.20, and 11.21, which shows the result of converting to double => Poppins: 12.8 pounds and to int => Poppins: 12 pounds.

# Applying Type Conversions Automatically

Listing 11.21 uses int(poppins) with cout. Suppose that instead, it omitted the explicit type cast:

```
cout << "Poppins: " << poppins << " pounds\n"
double p_wt = poppins;
```

Would the program use an implicit conversion, as in the following statement?

The answer is no. In the p_wt example, the context indicates that poppins should be converted to double. But in the cout example, nothing indicates whether the version should be to int or to double. Facing this lack of information, the compiler would complain that you were using an ambiguous conversion. Nothing in the statement indicates which type to use.

Interestingly, if the class defined only the double conversion function, the compiler would accept the statement. That’s because with only one conversion possible, there is no ambiguity.

You can have a similar situation with assignment. With the current class declarations, the compiler rejects the following statement as being ambiguous:

```
long gone = poppins; // ambiguous
```

In C++, you can assign both int and double values to a long variable, so the compiler can legitimately use either conversion function. If you eliminate one of the two conversion functions, the compiler accepts the statement. For example, suppose you omit the double definition. Then the compiler will use the int conversion to convert poppins to a type int value. Then it converts the int value to type long when assigning it to gone.

When the class defines two or more conversions, you can still use an explicit type cast to indicate which conversion function to use. You can use either of these type notations:

```
long gone = (double) poppins;   // use double conversion
long gone = int(poppins);    // use int conversion
```

The first of these statements converts poppins to a double value, and then assignment converts the double value to type long. Similarly, the second statement converts poppins first to type int and then to long.

Like constructors, conversion functions can be a mixed blessing. Problem with providing functions that make automatic conversions is that they may make conversions when you don't expect them. Suppose, for example, that you happen to write the following code when you're sleep deprived:

```
int ar[20];
Stonew temp(14, 4);
int Temp = 1;
cout << ar[temp] << "!\n";   // use temp instead of Temp
```

Normallly, you'd expect the compiler to catch a blunder such as using an object instead of an integer as an array index. The Stonew class defines an operator int(), so the Stonew object temp is converted to the int 20 and be used as an array index.
