# Chapter 10 Objects and Classes

Alternatively, you can use the keyword struct instead of class. In either case, you
now need to use the enum name to qualify the enumerator:

```
egg choice = Large; // the Large enumerator of the egg enum
t_shirt Floyd = t_shirt::Large; // the Large enumerator of the t_shirt enum
```

Now that the enumerators have scope, enumerators from different enum definitions
no longer have name conflicts, and your egg-and-shirt project can proceed.
C++11 also tightens up type security for scoped enumerations. Regular enumerations
get converted types automatically in some situations, as assignment to enumerations no
int variable or being used in a comparison, but scoped enumerations have
implicit conversions to integer types:

```
enum egg_old {Small, Medium, Jumbo}; // unscoped
enum t_shirt {Small, Medium, Large, XLarge}; // scoped
egg_old = Medium; // scoped
t_shirt rolf = t_shirt; // implicit type conversion for unscoped
int kind = rol; // not allowed, no implicit type conversion
if (kind < jumbo) // allowed
std::cout << "Jumbo converted to int before comparison.\n";nif (kind < t_shirt::Medium) // not allowed
std::cout << "Not allowed: not defined for scoped enum.\n";
```

But you can do an explicit type conversion if you have to:
int Frodo = int(t_shirt::Small); // Frodo set to 0

Enumerations are represented by unscoped integer type, and C98 that
choice was implementation-dependent. Thus, a structure containing an enumeration
of be different sizes on different systems. C++11 introduces that dependency for
scoped enumerations. By default, the underlying type for C++11 scoped enumerations is
int. Furthermore, there's a syntax for indicating a different choice:

```
// underlaying type for pizza is short
enum class : short {Small, Medium, Large, XLarge};
```

The : specifies the underlying type for pizza to be short. The underlying type has to be
an integer type. Under C++11, you can also use this syntax to indicate the underlying
type for an unscoped enumeration, but if you don't choose the type, the choice com-
piler is implementation-dependent.

# Abstract Data Types

The stack class is pretty specific. Often, programmers define classes to represent
more general concepts. For example, using classes is a good way to implement com-\puter scientists describe abstract data types (ADTs). As the name suggest, ADT
describes a type in a general fashion without bringing in language or implementa-
t details. Consider, for example, the stack. By using the stack, you can store data so that