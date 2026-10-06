# Solutions to Chapter 13 | C++

13.3 How do virtual functions work in C++?

# SOLUTION

A virtual function depends on a "vtable" or "Virtual Table". If any function of a class is declared as virtual, a v-table is constructed which stores addresses of the virtual functions of this class. The compiler also adds a hidden vptr variable in all classes which points to the vtable of that class. If a virtual function is not overridden in the derived class, the vtable of the derived class stores the address of the function in its parent class. The v-table is used to resolve the address of the function, for the virtual function is called. Dynamic binding in C++ is therefore performed through the vtable mechanism.

Thus, when we assign the derived class object to the base class pointer, the vptr points to the vtable of the derived class. This assignment ensures that the most derived virtual function gets called.

```
class Shape {
public:
    int edge_length;
    virtual int circumference() {
        cout << "Circumference of Base Class\n"
        return 0;
    }
}
class Triangle: public Shape {
public:
    int circumference() {
        cout << "Circumference of Triangle Class\n"
        return 3 * edge_length;
    }
}
void main() {
    Shape *x = new Shape();
    x->circumference(); // prints "Circumference of Base Class"
    Shape *y = new Triangle();
    y->circumference(); // prints "Circumference of Triangle Class"
}
```

In the above example, circumference is a virtual function in shape class, so it becomes virtual in each of the derived classes (triangle, rectangle). C++ non-virtual function calls are resolved at compile time with static binding, while virtual function calls are resolved at run time with dynamic binding.

![](bbox=[0.215, 0.845, 0.485, 0.895])