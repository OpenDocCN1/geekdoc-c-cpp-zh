
# Chapter 10 Objects and Classes

```cpp
class Ik
{
private:
    int fuss; // fuss has class scope
public:
    Ik(int f = 9) {fuss = f; } // fuss is in scope
    void ViewIk() const; // ViewIk has class scope
};
```

```cpp
void Ik::ViewIk() const //Ik: places ViewIk into Ik
{
    cout << fuss << endl; // fuss in scope within class methods
}
```

```cpp
int main()
{
    Ik *pik = new Ik;
    Ik ee = Ik(8); // constructor in scope because class name
    ee.ViewIk(); // class object brings ViewIk into scope
    pik->ViewIk(); // pointer-to-Ik brings ViewIk into scope
}
```

# Class Scope Constants

Sometimes it would be nice to have symbolic constants with class scope. For example, a class declaration might use the literal 30 to specify an array size. Because the constant is the same for all objects, it would be nice to create a single constant shared by all objects. You might think the following would be a solution:

```cpp
class Bakery
{
private:
    const int Months = 12; // declare a constant? FAILS
    double costs[Months];
}
```

But this won't work because declaring a class describes what an object looks like but doesn't create an object. Hence, until you create an object, there's no place to store a value. (Actually, C++11 provides for member initialization, but not in a way that would make the preceding array declaration work; Chapter 12 returns to this topic.) There are, however, a couple ways to achieve essentially the same desired effect.

First, you can declare an enumeration within a class. An enumeration declaration has class scope, so you can use enumerations to provide class scope symbolic names for integer constants. That is, you can start off the Bakery declaration this way:

# Class Scope

```cpp
class Bakery {
private:
    enum {Months = 12};
    double costs[Months];
    ...
};
```

Note that declaring an enumeration in this fashion does not create a data member. That is, each individual object does not carry an enumeration in it. Rather, Len is just a symbolic name that the compiler replaces with 30 when it encounters it in code class scope.

Because the Bakery uses the enumeration to create a symbolic constant, with no intent of creating variables of the enumeration type, you needn't provide an enumeration tag. Incidentally, for many implementations, the ios_base class does something similar in its public section such as ios_base::fixed. Here fixed is typically a second way of using enumerator defined in the ios_base class.

C++ has another way of defining a constant within a class—using the keyword static:

```cpp
class Bakery
private:
    static const int Months = 12;
    double costs[Months];
    ...
};
```

This creates a single constant called Months that is stored with other static variables rather than in an object. Thus, there is only one Months shared by all Bakery objects. Chapter 12 looks further into static class members. In C++98 you can use this technique for declaring static constants with integral and enumeration values. Thus, C++98 doesn't allow you to store a double constant this way. C++11 removes that restriction.

# Scoped Enumerations (C++11)

Traditional enumerations have some problems. One is that enumerators from two different definitions can conflict. Suppose you were working on a project involving eggs and T-shirts. You might try something like this:

```cpp
enum egg {Small, Medium, Large, Jumbo};
enum t_shirt {Small, Medium, Large, XLarge};
```

This won't fly because the egg and the t_shirt Small would both be in the same scope, and the names conflict. C++11 provides a new form of enumeration that avoids this problem by having class scope for its enumerators. The declarations for this form like this:

```cpp
enum class egg {Small, Medium, Large, Jumbo};
enum class t_shirt {Small, Medium, Large, XLarge};
```

# Chapter 10 Objects and Classes

Alternatively, you can use the keyword struct instead of class. In either case, you now need to use the enum name to qualify the enumerator:

```cpp
egg choice = Large; // the Large enumerator of the egg enum
t_shirt Floyd = t_shirt::Large; // the Large enumerator of the t_shirt enum
```

Now that the enumerators have scope, enumerators from different enum definitions no longer have name conflicts, and your egg-and-shirt project can proceed.
C++11 also tightens up type security for scoped enumerations. Regular enumerations get converted types automatically in some situations, as assignment to enumerations no int variable or being used in a comparison, but scoped enumerations have implicit conversions to integer types:

```cpp
enum egg_old {Small, Medium, Jumbo}; // unscoped
enum t_shirt {Small, Medium, Large, XLarge}; // scoped
egg_old = Medium; // scoped
t_shirt rolf = t_shirt; // implicit type conversion for unscoped
int kind = rol; // not allowed, no implicit type conversion
if (kind < jumbo) // allowed
std::cout << "Jumbo converted to int before comparison.\n";
if (kind < t_shirt::Medium) // not allowed
std::cout << "Not allowed: not defined for scoped enum.\n";
```

But you can do an explicit type conversion if you have to:
int Frodo = (int)t_shirt::Small; // explicit type conversion

Enumerations are not implicitly converted to integer types unless you use an explicit cast. This is because scoped enumerations are strongly typed.
