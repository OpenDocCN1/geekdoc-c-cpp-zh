The template member assignment operator, defined on lines [95-96], basically does something similar to the previous copy constructor. The only difference is line [99], which disallows copying of the same objects, called _self-assignment protection_. Although it looks unusual, such a situation can happen, for example, if a container of pointers to the objects is reorganized, sorted, etc. If the self-assignment fuse were omitted, then performing the code on line [102] would erroneously destroy the fractional part, which we would then try to copy on lines [104-105].

On lines [115-120] are declarations of the type-conversion operators whose role is to perform type conversion but in the opposite direction than the conversion constructor. They can convert an `FxFor` object into one of the integer types or the FP type, in this case.

```
```
// Conversion operators:
115 constexpr operator char() const;
116 constexpr operator short() const;
117 constexpr operator int() const;
118 constexpr operator long() const;
119 constexpr operator double() const;
```
```