# Listing 2.10 Enforcing restrictions on the data members of a class

```
d1.setFeet(1);
d1.setInches(9.5);
d2.setFeet(2);
d2.setInches(5.5);
d3=d1.add(d2);
```

then the value of d3.fInches will become 3 (not 15) and the value of d3.iFeet will become 4 (not 3).
It has already been mentioned that real-world objects never avoid an invalid state. They also do not start in an invalid state. Does C++ enable the library programmer to implement this feature in class objects?
Let us continue with our earlier example—the Distance class. Recall that it is the library programmer's intention to ensure that the value of fInches portion of none of the objects of the class Distance should exceed 12. Now, let us consider Listing 2.11.

# Listing 2.11 Object created with improper values

```
/Beginning of DistJunk.cpp*/n#include<iostream>
#include="Distance.h"
void main()
{
    Distance d1;
    cout<<d1.getFeet()<<""<<d1.getInches()<<endl;
}
/End of DistJunk.cpp*/
```

# Output
29 34.56

As you can see, the value of fInches of ‘d1’ is larger than 12! This happened because the value of both iFeet and fInches automatically got to junk values when ‘d1’ was allocated memory and the junk value is larger than 12 for d1.fInches. Thus, the objective of the library programmer to keep the value of fInches less than 12 has not been achieved.
It would be unrealistic to expect that an application programmer will explicitly initialize each object that is declared.

```
Distance d1; //initialization
d1.setFeet(0.0); //initialization
```

Obviously, the library programmer would like to add a function to the Distance class that gets called automatically when an object is created and sets the values of the data members of the object property. Such a function is the *constructor*. The concept of constructor and a related function, the *destructor*, is discussed in one of the later chapters.
But may say that even if Distance was an ordinary structure and setInches() function was a non-member function just as in C, data abstraction would be in place. Nevertheless, in the case of C, the library programmer cannot force calls to only those functions that have been defined.