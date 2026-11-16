For many abstract types it can be possible to define an ordering. For dates there is the natural ordering. C++ Code 1.3 shows how such comparison operations is defined.

```
#include "date.h"

bool operator ==(const date& d1,const date& d2){ // check for equality
 if ( (!d1.valid()) && (!d2.valid()) ) { return false; }; /* if dates not valid, not clear what to do.
 alternative: throw exception */
 return ((d1.day())==d2.day()) && (d1.month())==d2.month()) && (d1.year())==d2.year()));
};

bool operator <(const date& d1, const date& d2){
 if ( (!d1.valid()) && (!d2.valid()) ) { return false; }; // see above remark
 if (d1.year())==d2.year()) { // same year
   if (d1.month())==d2.month()){ // same month
     return (d1.day()<d2.day());
   }
   else {
     return (d1.month()<d2.month());
   }
 }
 else { // different year
   return (d1.year()<d2.year());
 }
};

// remaining operators defined in terms of the above

bool operator <=(const date& d1, const date& d2){
 if (d1==d2) { return true; }
 return (d1<d2);
}

bool operator >(const date& d1, const date& d2) {
 if (d1==d2) { return true; }
 return (d1>d2);
};

bool operator >(const date& d1, const date& d2) { return !(d1<=d2);};
bool operator !=(const date& d1, const date& d2){ return !(d1==d2);};
```

C++ Code 1.3: Comparison operators for the date class