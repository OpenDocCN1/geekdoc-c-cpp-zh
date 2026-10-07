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
-Stonew();
void show_lbs(const) const;               // show weight in pounds format
void show_stn(const) const;               // show weight in stone format
```

conversion functions
operator int() const;
operator double() const;

};
#endif

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
    stone = int (lbs) / Lbs_per_stn;      // integer division
    pds_left = int (lbs) % Lbs_per_stn + lbs - int (lbs);
    pounds = ++;n}

// construct Stonew object from stone, double values
Stonew::Stonew(int stn, double lbs)
{
    stone = stn;
    pds_left = lbs;
    pounds = stn * Lbs_per_stn +lbs;
}
```