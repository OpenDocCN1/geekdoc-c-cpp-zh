Alternatively, you can use the keyword `struct` instead of `class`. In either case, you now need to use the enum name to qualify the enumerator:

```
```cpp
egg choice = egg::Large;        // the Large enumerator of the egg enum
t_shirt Floyd = t_shirt::Large; // the Large enumerator of the t_shirt enum
```
```

Now that the enumerators have class scope, enumerators from different enum definitions no longer have potential name conflicts, and your egg-and-T-shirt project can proceed. C++11 also tightens up type security for scoped enumerations. Regular enumerations get converted to integer types automatically in some situations, such as assignment to an `int` variable or being used in a comparison expression, but scoped enumerations have no implicit conversions to integer types:

```
```cpp
enum egg_old {Small, Medium, Large, Jumbo};     // unscoped
enum class t_shirt {Small, Medium, Large, XLarge}; // scoped
egg_old one = Medium;                            // unscoped
t_shirt roll = t_shirt::Large;                   // scoped
int king = one;       // implicit type conversion for unscoped
int ring = roll;      // not allowed, no implicit type conversion
if (king == Jumbo)
    std::cout << "Jumbo converted to int before comparison.\\n";
if (king < t_shirt::Medium)  // not allowed
    std::cout << "Not allowed: < not defined for scoped enum.\\n";
```
```

But you can do an explicit type conversion if you feel you have to:

```
```cpp
int Frodo = int(t_shirt::Small); // Frodo set to 0
```
```

Enumerations are represented by some underlying integer type, and under C98 that choice was implementation-dependent. Thus, a structure containing an enumeration might be of different sizes on different systems. C++11 removes that dependency for scoped enumerations. By default, the underlying type for C++11 scoped enumerations is `int`. Furthermore, there’s a syntax for indicating a different choice:

```
```cpp
// underlying type for pizza is short
enum class pizza : short {Small, Medium, Large, XLarge};
```
```

The `: short` specifies the underlying type to be short. The underlying type has to be an integer type. Under C++11, you also can use this syntax to indicate the underlying type for an unscoped enumeration, but if you don’t choose the type, the choice the compiler makes is implementation-dependent.

# Abstract Data Types

The `Stock` class is pretty specific. Often, however, programmers define classes to represent more general concepts. For example, using classes is a good way to implement what computer scientists describe as *abstract data types* (ADTs). As the name suggests, an ADT describes a data type in a general fashion without bringing in language or implementation details. Consider, for example, the stack. By using the stack, you can store data so that