```
```cpp
class Car : private Engine {    // Car has a engine
public:
  Car() : Engine{8} { }        // initializes a car with 8 cylinders
    using Engine::start;       // starts car by starting the engine
};
```
```

Listing 18.7 A has-a relationship via private inheritance.

Here you see another use of using. There are several situations where a method from the base class is no longer visible—and this is one of them. The start method from Engine is usually only private in Car because Engine was included with private inheritance—a has-a inheritance. To make the public method visible in Car, you can declare the start identifier from Engine with using Engine::start within the appropriate section. If there are multiple overloads of start, all are automatically included. Alternatively, you can make it more explicit by overriding the method as void start() ( Engine::start(); ).

# Shadowing

A brief excursion: it is possible to override a method in a derived class while giving it a different signature. The overridden version is then shadowed—it is hidden and no longer visible:

```
```cpp
// https://godbolt.org/z/Gb3zx1j7
#include <string>
struct Base {
    void func(int x) {};
};
struct Derived : public Base {
    void func(std::string y) {};   // shadows func(int)
};
int main() {
    Derived d;
    d.func("Text");
    d.func(3);                     // ❌ Error: func(int) is no longer visible
}
```
```

The d.func(3) call can no longer see the func(int) overload. You would need to remove the definition of func(string) in the Derived class for it to work again (and delete d.func("Text") in main()).

Shadowing methods in this way is usually not desirable. You should assign new names. If you want to override and use virtual methods, then use overload to ensure you are really overriding.