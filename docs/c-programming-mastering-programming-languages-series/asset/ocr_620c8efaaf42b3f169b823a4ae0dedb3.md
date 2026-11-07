```
```cpp
int main() {
    // Creating an object of the derived class
    Circle myCircle;

    // Using a pointer to the base class for polymorphism
    Shape* ptrShape = &myCircle;
    ptrShape->draw(); // Calls the draw function of Circle

    return 0;
}
```
```

Here, the Shape class is an abstract class with a pure virtual function draw(). The Circle class derives from Shape and provides a concrete implementation for the draw() function. Objects of abstract classes cannot be instantiated, but pointers to the base class can be used for polymorphism.

Understanding virtual functions and abstract classes is fundamental for harnessing the power of polymorphism in C++. These concepts form the bedrock of designing flexible and extensible class hierarchies, enabling developers to create software architectures that can adapt to changing requirements.