For this, we must overload the addition operator for the class Distance by using either a member function or a friend function.

Let us first look at a member function to overload the addition operator for the class Distance. In this case, the statement

```
d3 = d1 + d2;
```

will be interpreted as

```
d3 = d1.operator + (d2);
```

This obviously means that the function must return an object of the class Distance and must accept an object of the class Distance as a parameter. The actual code to implement the addition operator so that it produces the desired effect described is given in Listing 8.20.

**Listing 8.20** Overloading the addition operator for the class Distance through function

```
/*Beginning of Distance.h*/
class Distance {
    int iFeet;
    float inches;
    public:
        Distance(const int=0, const float=0.0);
        void setFeet(const int=0);
        int getFeet() const;
        void setInches(const float=0.0);
        float getInches() const;
        //prototype
        Distance operator + (const Distance) const;
};
/*End of Distance.h*/
```

```
/*Beginning of Distance.cpp*/
#include "Distance.h"
//definition
Distance Distance::operator+(const Distance d1) const {
    return Distance(iFeet+d1.iFeet, inches+d1.inches);
}
/*
definitions of the rest of the functions of class Distance
*/
/*End of Distance.cpp*/
```

The code in Listing 8.20 works if the right-hand side of addition operator is an object of class Distance. However, if it is a float-type value, the preceding function will work.

```
d3=d1+4.5;
```

This is because the compiler will interpret this statement as follows:

```
d3=d1.operator+(4.5);
```

The float-type value 4.5 will be passed as a parameter to the operator-overloading function. Since the formal argument of the operator-overloading function is a Distance type object,