
We’ve seen an initial example of the use of this principle in section 9.7.4. Of course, the principle cannot be applied to the copy constructor itself, as you need a copy constructor to make a copy. The copy- and move constructors must always be implemented independently from each other.

## 9.8 Copy Elision and Return Value Optimization

When the compiler selects a member function (or constructor) it applies a simple set of rules, matching arguments with parameter types.

Below two tables are shown. The first table should be used in cases where a function argument has a name, the second table should be used in cases where the argument is anonymous. In each table select the const or non-const column and then use the topmost overloaded function that is available having the specified parameter type.

The tables do not handle functions defining value parameters. If a function has overloads expecting, respectively, a value parameter and some form of reference parameter the compiler reports an ambiguity when such a function is called. In the following selection procedure we may assume, without loss of generality, that this ambiguity does not occur and that all parameter types are reference parameters.

Parameter types matching a function’s argument of type T if the argument is:

- a *named* argument (an lvalue or a named rvalue)

|  | the argument is: non-const | the argument is: const |
|---|---|---|
| Use the topmost available function | `T &` | `T const &` |

Example: for an `int x` argument a function `fun(int &)` is selected rather than a function `fun(int const &)`. If no `fun(int &)` is available the `fun(int const &)` function is used. If neither is available the compiler reports an error.

- an *anonymous* argument (an anonymous temporary or a literal value)

|  | the argument is: non-const | the argument is: const |
|---|---|---|
| Use the topmost available function | `T &&` | `T const &&` |
| available function | `T const &` | `T const &` |

Example: when the return value of an `int arg()` function is passed to a function `fun` for which various overloaded versions are available `fun(int &&)` is selected. If this function is unavailable but `fun(int const &)` is, then the latter function is used. If none of these two functions is available the compiler reports an error.

The tables show that eventually *all* arguments can be used with a function specifying a `T const &` parameter. For *anonymous* arguments a similar *catch all* is available having a higher priority: `T const &&` matches all anonymous arguments. Functions having this signature are normally not defined as their implementations (should be) identical to the implementations of the functions expecting a `T const &` parameter. Since the temporary can apparently not be modified, a function defining a `T const &&` parameter has no alternative but to copy the temporary’s resources. As this task is already performed by functions expecting a `T const &`, there is no need for implementing functions expecting `T const &&` parameters.

As we’ve seen, the move constructor grabs the information from a temporary for its own use. That is OK as the temporary is going to be destroyed after that anyway. It also means that the temporary’s data members are modified.

Having defined appropriate copy and/or move constructors, it may be somewhat surprising to learn that the compiler may decide to stay clear of a copy or move operation. After all, making *no* copy and *not* moving is more efficient than copying or moving.

The option the compiler has to avoid making copies (or performing move operations) is called *copy elision* or *return value optimization*. In all situations where copy or move constructions are appropriate, the compiler may apply copy elision. Here are the rules. In sequence the compiler considers the following options, stopping once an option can be selected:

- if a copy or move constructor exists, try copy elision
- if a move constructor exists, move.
- if a copy constructor exists, copy.
- report an error

All modern compilers apply copy elision. Here are some examples where it may be encountered:

```
class Elide;

Elide fun()          // 1
{
    Elide ret;
    return ret;
}

void gun(Elide par);

Elide elide(fun()); // 2

gun(fun());          // 3
```

- At 1 `ret` may never exist. Instead of using `ret` and copying `ret` eventually to `fun`’s return value it may directly use the area used to contain `fun`’s return value.
- At 2 `fun`’s return value may never exist. Instead of defining an area containing `fun`’s return value and copying that return value to `elide` the compiler may decide to use `elide` to create `fun`’s return value in.
- At 3 the compiler may decide to do the same for `gun`’s `par` parameter: `fun`’s return value is directly created in `par`’s area, thus eliding the copy operation from `fun`’s return value to `par`.

## 9.9 Plain Old Data (C++11)

C++ inherited the struct concept from C and extended it with the class concept. Structs are still used in C++, mainly to store and pass around aggregates of different data types. A common term for these structs is *plain old data* (pod). Plain old data is commonly used in C++ programs to aggregate data. E.g., when a function needs to return a `double`, `bool` and `std::string` these three different data types may be aggregated using a `struct` that merely exists to pass along values. Data protection and functionality is hardly ever an issue. For such cases C and C++ use `structs`. But as a C++ struct is just a class with special access rights some members (constructors, destructor, overloaded assignment operator) may implicitly be defined. The plain old data capitalizes on this concept by requiring that its definition remains as simple as possible. Specifically the C++11 standard considers pod to be a class or struct having the following characteristics:

- it has a trivial default constructor.

  If a type has some *trivial member* then the type (or its base class(es), cf. chapter [13](#)) does not explicitly define that member. Rather, it is supplied by the compiler. A trivial default constructor leaves all its non-class data members uninitialized and calls the default constructors of all its class data members. A class having a trivial default constructor does not define any constructor at all (nor do its base class(es)). It may also define the default constructor using the default constructor syntax introduced in section 7.5;

- it has a trivial copy constructor.

  A trivial copy constructor byte-wise copies the non-class data members from the provided existing class object and uses copy constructors to initialize its base class(es) and class data members with the information found in the provided existing class object;

- it has a trivial overloaded assignment operator.

  A trivial assignment operator performs a byte-wise copy of the non-class data members of the provided right-hand class object and uses overloaded assignment operators to assign new values to its class data members using the corresponding members of the provided right-hand class object;

- it has a trivial destructor.

  A trivial destructor calls the destructors of its base class(es) and class-type data members;

- it has a *standard layout*.

A *standard-layout* class or struct

- has only non-static data members that are themselves showing the *standard-layout*;
- has identical access control (public, private, protected) for all its non-static members;

Furthermore, in the context of class derivation (cf. chapters 14 and 13), a *standard-layout* class or struct:

- has only base classes that themselves show the *standard-layout*;
- has at most one (in)direct base class having non-static members;
- has no base classes of the same type as its first non-static data member;
- has no virtual base classes;
- has no virtual members.

## 9.10 Conclusion

Four important extensions to classes were introduced in this chapter: the destructor, the copy constructor, the move constructor and the overloaded assignment operator. In addition the importance of *swapping*, especially in combination with the overloaded assignment operator, was stressed.

Classes having pointer data members, pointing to dynamically allocated memory controlled by the objects of those classes, are potential sources of memory leaks. The extensions introduced in this chapter implement the standard defense against such memory leaks.

Encapsulation (data hiding) allows us to ensure that the object's data integrity is maintained. The automatic activation of constructors and destructors greatly enhance our capabilities to ensure the data integrity of objects doing dynamic memory allocation.

A simple conclusion is therefore that classes whose objects allocate memory controlled by themselves must at least implement a *destructor*, an *overloaded assignment operator* and a *copy constructor*. Implementing a *move constructor* remains optional, but it allows us to use *factory functions* with classes *not* allowing copy construction and/or assignment.
