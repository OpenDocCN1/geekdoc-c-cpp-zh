members are restricted to the class itself, and protected members allow controlled access in the context of inheritance. Proper use of access specifiers contributes to code clarity, maintainability, and the overall integrity of object-oriented designs.

# Accessors and Mutators (Getters and Setters)

Accessors and mutators, commonly known as getters and setters, are essential components in object-oriented programming for managing the access and modification of private data members within a class. This section explores the significance of accessors and mutators, emphasizing their role in maintaining encapsulation, controlling data integrity, and facilitating proper interaction with class members.

# Accessors: Retrieving Private Data Safely

Accessors, often referred to as getter methods, provide a controlled means to retrieve the values of private data members from outside the class. By encapsulating data access within member functions, classes can ensure that external code interacts with the data in a controlled and consistent manner. Consider the following example:

```
```cpp
#include <iostream>

// Class with private data and accessor
class Person {
private:
    // Private data member
    std::string name;

public:
    // Accessor (getter) for the private data member
    std::string getName() const {
        return name;
    }

    // Member function to display information
    void displayInfo() const {
        std::cout << "Person's name: " << name << std::endl;
    }
};

int main() {
    // Creating an object of the Person class
    Person individual;
```
```