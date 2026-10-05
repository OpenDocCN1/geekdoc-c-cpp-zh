
```cpp
class Value {
    int val;
public:
    constexpr Value(int val) : val_{val} {};
    constexpr int get() const { return val_; }
};

constexpr Value five{5}; // works, Value is a literal data type
std::array<int,five.get()> data; // works, get is constexpr
```

**Listing 18.20** You create a literal data type with a constexpr constructor.

It is only because the constructor of Value is marked with constexpr that you are allowed to write constexpr Value five at all. This, in turn, is a condition for use as a template parameter. If five were not constexpr, you could not write array<...>. But also, the get must be constexpr here; otherwise, the compiler would not be able to get the value for the template parameter at compile time.

Literal data types are especially useful when you also define-defined literals for them.

```cpp
// https://godbolt.org/z/rlvYcr75j
#include <array>
#include <iostream>
#include <type_traits> // is_literal_type
class Value {
    int val;
public:
    constexpr Value(int val) : val_{val} {};
    constexpr operator int() const { return val_; }
};
namespace lit {
    constexpr Value operator*"_val(const char*, size_t sz) {
        return Value(sz);
    }
}
struct Node {
    constexpr Node() {};
    virtual ~Node() {}; // non-constexpr destructor
};
int main() {
  using namespace lit;
  constexpr Value five{5};
  std::array<int,"11111"_val> data; // use user-defined literal
  std::cout << data.size() << '\n'; // Output: 5
  std::cout << std::boolalpha;
  std::cout << std::is_literal_type<Value>::value << '\n'; // Output:
true
false
  std::cout << std::is_literal_type<None>::value << '\n'; // Output:
}
```

# Listing 18.21

User-defined literals are especially useful with literal data types.

Doesn't it seem interesting that you can use "11111"_val as a continuous chain parameter? That's because there is a continuous chain of constexpr expressions up to the return val_.

Note that you can only make particularly simple classes with a constexpr constructor into a literal data type. For example, all data fields must also be literal types. A (non-constexpr) destructor prevents such usage.

By the way, you can find out if a type is suitable as a literal data type by using the type trait is_literal_type. In the example, you can see this with None.

# 19 GOOD CODE, 5TH DAN: CLASSICAL OBJECT-ORIENTED DESIGN

# Chapter Telegram

- Object-oriented programming (OOP)
Object-oriented programming.

- SOLID
Acronym for five important OOP principles that help in the design of large projects.

- Single responsibility principle (SRP)
A class should have only one reason to change.

- Open/closed principle (OCP)
Classes, functions, and modules should be open for extensions but closed for modifications.

- Liskov substitution principle (LSP)
Instances of a derived type should be able to replace instances of the base type.

- Interface segregation principle (ISP)
No client should be forced to depend on methods it does not use.

- Dependency inversion principle
Modules should depend on abstractions, not on other modules.

- Covariance
Return types can be more specific than those of the supertype.

- Contravariance
Arguments can be more general than those of the supertype.

- Model-view-controller (MVC)
MVC is a popular architectural pattern.

Chapter 15, you have seen how to derive classes from each other in C++ using *inheritance*. In very brief terms, I also explained some central concepts of *object-oriented programming* there, particularly the difference between the *has-a* relationship and the *is-a* relationship.

However, there is more to OOP:

- Abstraction
You find commonalities between your objects, defining their methods and functions as generally and generically as possible.

- Class
A class defines the commonalities of a category of objects. This class concept is reflected in C++ in a class.

- Encapsulation
When you combine elements into a new entity, you form a capsule. So, when you define data and methods of a class, you *encapsulate*. Objects know themselves, in C++ as *this*, and manipulate only their own data directly.

- Information hiding
You choose which part of a class and method should be visible externally, thus forming the interface. You reveal only as much as other classes need, no more.

- Inheritance
A class inherits the implementation of its base class.

This represents the is-a relationship.

- Interface
The communication interface of your program to the outside.

- Messages
Objects communicate with each other by sending messages to their respective interfaces. In C++, they call methods of other objects for this purpose.

- Object
A closed unit of data and behavior—in C++, the instance of a class. In OOP, the data of objects are often called *fields* or *attributes*. The behavior is defined in C++ using methods on the class or free functions—OOP calls these both *procedures*.

- Polymorphism
The ability of a program to behave differently with different objects.

- Modularization
More manageable units of the program through abstraction and division into classes.

The motivation for OOP is the better reusability of programs or modules. Abstraction should help solve problems that have already been solved with the same program code. For this to work, clean encapsulation and information hiding are necessary to minimize dependencies between program parts.

Instead of changing the individual bits and bytes of a large global state while programming, you take a step back by sending messages and look at the bigger picture. The object that receives the message is responsible for the internal details. Other objects mainly need to take care of the relationships.

By having the code more cleanly divided with fewer dependencies, the maintainability is also increased.

# 19.1 Objects in C++

In C++, OOP is represented with classes. A class is the blueprint for objects. The behavior is firmly programmed via methods, and the data is included as fields and thus as placeholders in the class definition.

When you instantiate a class, the fields are filled with concrete data, and you get a concrete object—that is, an instance of a class.

```cpp
VwBus bus(green, 120 km); // automatic variable
Car *modelT = new ModelT(black, 80 km); // dynamically managed
```

When instantiating, it doesn't matter whether you do this as an automatic variable or if it's dynamically managed. However, if you define a car as a value parameter, then you will always get a car, never a VWBus or ModelT.

```cpp
// https://godbolt.org/z/71fE4zj
class Car { };
```

```cpp
class VwBus : public Car { };
class ModelT : public Car { };

void letDrive(Car vehicle) { // Value parameter copies only base
void letBrake(Car &vehicle) { // Reference parameter
void letHonk(Car *vehicle) { // Passed as pointer
int main() {
    VwBus bus; // automatic variable
    Car *modelT = new ModelT(); // dynamically managed
    letDrive(bus); // gets copied to Car
    letDrive(*modelT); // gets copied to Car
    letBrake(bus); // remains VwBus
    letBrake(*modelT); // remains ModelT
    letHonk(&bus); // remains VwBus
    letHonk(modelT); // remains ModelT
}
```

# Listing 19.1 Call-by-reference as a basis for polymorphism.

Because the parameter is defined as a value parameter in letDrive(), C++ copies using the copy constructor. And the responsibility for how to copy lies with the object that is needed within letDrive()—and that is a Car. So it is the copy constructor of the Car class that is used here. But it only knows how to copy Car, not VwBus or ModelT.

However, if you pass a reference into a function like letBrake(), nothing needs to be copied, so the vehicle remains exactly the type it was outside.
