```
```cpp
public:
void bark() {
cout << "Dog is barking." << endl;
}
};
```
```

In this example, Dog is a derived class that inherits the eat function from the Animal base class. This relationship allows Dog to both use the existing functionality of Animal and introduce its own unique behaviours.



Polymorphism allows objects of different types to be treated as objects of a common type. This is achieved through two mechanisms: function overloading and virtual functions.

# **Function Overloading:**

```
```cpp
class Calculator {
public:
int add(int a, int b) {
return a + b;
}
double add(double a, double b) {
return a + b;
}
};
```
```

Here, the add function is overloaded to handle both integer and floating-point additions. The appropriate version is selected based on the types of arguments provided.

# **Virtual Functions:**

```
```cpp
// Base class with a virtual function
class Shape {
public:
virtual void draw() {
cout << "Drawing a shape." << endl;
}
};

// Derived class overriding the virtual function
class Circle : public Shape {
};
```
```