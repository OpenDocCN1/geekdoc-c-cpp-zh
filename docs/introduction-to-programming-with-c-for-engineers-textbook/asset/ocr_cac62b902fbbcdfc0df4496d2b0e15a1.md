Note that in addition to the previous two classes, TLongNumberFor defines its own internal NibbleArray. These two are joined by the aggregation relation since the latter’s existence is strictly related to the lifetime of the former.

We will now consider the two possible implementations, considering their benefits and drawbacks.

# 4.15.4.1  Aggregating PESEL

Listing 4.35 shows the definition of the PESEL class, which simply embeds the TLongNumberFor< 11 > object, as shown in Figure 4.23a. Hence, PESEL “has” the object of the TLongNumberFor type. In this case, a simpler version of TLongNumberFor is sufficient, so the ALLOW_INHERITANCE flag is set to 0 on line [1]. Then, the LongNumberFor.h header is included on line [2].

The alias and the TLongNumberFor object are created on lines [20–21]. Then, two constructors are used on line [25–26]. Finally, since the PESEL ID number contains encoded information about

```
```cpp
#define ALLOW_INHERITANCE 0
#include "LongNumberFor.h"

//////////////////////////////
// The "has-a" version
class PESEL
{
    private:

        // Some constants specific to the Polish PESEL number
        enum { kBirthYear_Dec = 10, kBirthYear_Sngl = 9, kSex = 1 };

    public:

        enum class ESex { kMan, kWoman };

    private:

        using LongNumberObject = TLongNumberFor< 11 >;
        LongNumberObject      fData;

    public:

        PESEL( void ) {}
        PESEL( const string & s ) : fData( s ) {}

    public:

        auto GetYearOfBirth( void )
        {
            return     fData.GetNumberAt( kBirthYear_Dec ) * 10
                     + fData.GetNumberAt( kBirthYear_Sngl );
        }

        ESex GetSex( void )
        {
            return      fData.GetNumberAt( kSex ) & 0x01 ) == 0x01 ?
                        ESex::kMan : ESex::kWoman;
        }
};
```
```