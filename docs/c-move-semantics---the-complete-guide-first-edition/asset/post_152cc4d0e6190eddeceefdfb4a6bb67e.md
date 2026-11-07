
```cpp
}
};
```

In this class, we usually make sure that the member val and the member sval are just two different representations of the same value. That means that in the implementation and use of this class, we usually expect that both the int and the string representation of its state are consistent. However, if we call a move operation here, we will keep the value val, but sval will no longer be guaranteed to have the string representation of val.

Consider the following program:

*basics/intstring.cpp*

```cpp
#include "intstring.hpp"
#include <iostream>

int main()
{
    IntString is1{42};
    IntString is2;
    std::cout << "is1 and is2 before move:\n";
    is1.dump();
    is2.dump();

    is2 = std::move(is1);

    std::cout << "is1 and is2 after move:\n";
    is1.dump();
    is2.dump();
}
```

This program typically has the following output (do not forget that a moved-from string becoming empty is typical but not guaranteed):

```text
is1 and is2 before move:
  [42/'42']
  [0/'0']
is1 and is2 after move:
  [42/'']
  [42/'42']
```

That is, the automatically generated move operation breaks our invariant that both members always match each other.

How big is this problem? Well, it is at least a possible trap. Again, you might argue that after a move we should no longer use the value (until we set the value again). However, programmers might expect a policy such as the one for objects of the C++ standard library, which states that objects are in a valid but unspecified state.

The fact is that with corresponding getters, the class no longer guarantees that the value as int and string match, which is probably a class invariant here (implicitly or explicitly stated). You might think that the worst consequence is that the value (which is unspecified now) looks different depending on how you use it, but there is no problem using it because it is still a valid int or string.

However, code counting on this invariant might be broken. That code might assume that the string representation has at least one digit. For example, if it searches for the first or last digit, you will definitely find one. For a moved-from string, which is typically empty, this is no longer the case. Therefore, code not double-checking whether there is any character in the string value, might run into unexpected undefined behavior.

Again, it is up to the designer of the class how to deal with this problem. However, if you follow the rule of the C++ standard library, you should leave your moved-from object in a valid state, which might mean that you introduce a precise state that represents “I do not have any value.”

In general, when the state of an object has members that depend on each other in some way, you have to explicitly ensure that the moved-from state is in a valid state. Examples where this might be broken are:

- We have different representations of the same value but some of them were moved away.
- A member such as a counter corresponds with the number of elements in a member.
- A Boolean value claims that a string value was validated but the validated value was moved away.
- A cached value for the average values of all elements is still there but the values (being in a container member) were moved away.

Note again that this class worked fine before C++11, where move semantics were not supported. The invariant is broken when switching to C++11 or later and moved-from objects are used.

## 6.3.3 Breaking Invariants Due to Moved Pointer-Like Members

The third reason for move operations breaking invariants relates to objects with members that have pointer-like semantics such as a (smart) pointer.

Consider the following example of a class where objects use a `std::shared_ptr<>` to share an integral value:

```cpp
class SharedInt {
private:
    std::shared_ptr<int> sp;
public:
    explicit SharedInt(int val)
        : sp{std::make_shared<int>(val)} {
    }

    std::string asString() const {
        return std::to_string(*sp);    // OOPS: assume there is always an int value
    }
};
```

The objects of this class receive an initial integral value that can be shared with copies of these objects. As long as new objects are only copied, everything is fine:

```cpp
SharedInt si1{42};
SharedInt si2{si1};                    // si1 and si2 share the value 42

std::cout << si1.asString() << '\n';  // OK
```

Being only copied, the SharedInt member sp always has allocated memory for its value (either from std::make_shared<> or from copying an existing shared pointer with allocated memory).

However, the moment we use move semantics, we run into undefined behavior if we still use the moved-from object:

```cpp
SharedInt si1{42};
SharedInt si2{std::move(si1)};          // OOPS: moves away the allocated memory in si1

std::cout << si1.asString() << '\n';  // undefined behavior (probably core dump)
```

The problem is that inside the class, we do not deal correctly with the fact that the value might have been moved away, which can happen because the default generated move operations call the move operations of the shared pointer, which moves the ownership away from the original object. This means that the moved-from state of a SharedInt brings the member sp into the situation where it no longer owns an object, which is not handled properly in its member function asString().

You might argue that calling asString() for an object with a moved-from state makes no sense because you are using an unspecified value, but at least the standard library guarantees for its types that moved-from types are in a valid state so that you can call all operations that have no constraints. Not giving the same guarantee in a user-defined type can be surprising for users of the type.

From a perspective of robust programming (avoiding surprises, traps, and undefined behavior), I would usually recommend that you follow the rule of the C++ standard library. That is: move operations should not bring objects into a state that breaks invariants.

In this case, we have to do one of the following:

- Fix all broken operations of the class by also dealing correctly with all possible moved-from states
- Disable move semantics so that there is no optimization when copying objects
- Implement move operations explicitly
- Adjust and document the invariant (constraints/preconditions) for the class or specific operations (such as “It is undefined behavior to call asString() for a moved-from object”)

Because allocating memory is expensive, probably the best fix in this case is to deal correctly with the fact that the ownership of the integral value might be moved away. That would create a state that a default constructor would have, which we could introduce with this change.

The following subsection demonstrates this and the other code fixes.

### Fixing Broken Member Functions

The first option, fixing all broken operations, essentially means that we extend the invariant of the class (possible states of all objects) so that all operations can deal with a moved-from state. We still have to make design decisions. For example, when calling `asString()` for a moved-from object (or more generally, an object where the shared pointer does not own an integral value), we can:

- Still return a fallback value:

```cpp
class SharedInt {
    ...
    std::string asString() const {
        return sp ? std::to_string(*sp) : "";
    }
    ...
};
```

- Throw an exception:

```cpp
class SharedInt {
    ...
    std::string asString() const {
        if (!sp) throw;
        return std::to_string(*sp);
    }
    ...
};
```

- Force a runtime error in debug mode:

```cpp
class SharedInt {
    ...
    std::string asString() const {
        assert(sp);
        return std::to_string(*sp);
    }
    ...
};
```

### Disabling Move Semantics

The second option is to disable move semantics so that only copy semantics can be used. We described earlier how to disable move semantics. You have to user-declare another special member function. Usually, you `=default` the copying special member functions:

```cpp
class SharedInt {
    ...
    SharedInt(const SharedInt&) = default;          // disable move semantics
    SharedInt& operator=(const SharedInt&) = default; // disable move semantics
    ...
};
```
