of both classes can be treated uniformly, and the appropriate version
of the draw() function is called at runtime based on the actual type of
the object.

# Function Overriding in Derived Classes

Function overriding allows a derived class to provide a specific
implementation for a function that is already defined in its base class.
To achieve this, the function in the base class must be declared as
virtual. The derived class then uses the override keyword to indicate
that it is intentionally overriding a virtual function.

```
```cpp
#include <iostream>

// Base class with a virtual function
class Animal {
public:
    // Virtual function for making a sound
    virtual void makeSound() const {
        std::cout << "Generic animal sound." << std::endl;
    }
};

// Derived class overriding the makeSound function
class Dog : public Animal {
public:
    // Overriding the makeSound function for dogs
    void makeSound() const override {
        std::cout << "Woof! Woof!" << std::endl;
    }
};

int main() {
    // Creating objects of base and derived classes
    Animal genericAnimal;
    Dog myDog;

    // Polymorphic behavior - calling makeSound on objects of different types
    genericAnimal.makeSound();
    myDog.makeSound();

    return 0;
}
```
```

In this example, the Animal class has a virtual function makeSound(),
and the Dog class overrides this function to provide a specific
implementation for the sound that dogs make. Through