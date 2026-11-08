
```cpp
// https://godbolt.org/z/xVtsveGjT
#include <vector>
#include <memory>        // unique_ptr
#include <iostream>      // cout
enum class ShapeTag { CIRC, RECT };
struct Shape {             // Data
    ShapeTag tag_;
    double v1_, v2_;
    Shape(double w, double h) : tag_{ShapeTag::RECT}, v1_{w}, v2_{h} {}
    Shape(double r) : tag_{ShapeTag::CIRC}, v1_{r}, v2_{0} {}
};
class AreaCalculator {     // Logic
public:
    double area(const std::vector<std::unique_ptr<Shape>>& shapes) const {
        double result = 0;
        for(auto &shape : shapes) {
            switch(shape->tag_) {
                case ShapeTag::CIRC:
                    result += 3.1415 * shape->v1_ * shape->v1_;
                    break;
                case ShapeTag::RECT:
                    result += shape->v1_*shape->v2_;
                    break;
            }
        }
        return result;
    }
};
int main() {
    std::vector<std::unique_ptr<Shape>> data{};
    data.push_back(std::make_unique<Shape>(10.));        // a circle
    data.push_back(std::make_unique<Shape>(4., 6.));    // a rectangle
    // calculate
    AreaCalculator calc{};
    std::cout << calc.area( data ) << "\n";
}
```

**Listing 19.4** Does not follow the open/closed principle.

The Shape “class” is a pure data class here. The data here means that either a rectangle or a circle is stored. Which one is indicated by tag_. Depending on whether only one data element for the radius is needed for a circle or two data elements for height and width are needed for a rectangle, either only v1_ or both v1_ and v2_ are relevant for the size specification.

The program or business logic is cleanly separated from the data. The area method in `AreaCalculator` calculates the sum of the areas of a vector. To do this, it must examine the `tag_` of each `Shape` and then decide whether to use the area formula for a circle or the formula for a rectangle.

## Why “unique_ptr”?

This example would also work with `vector<Shape>` instead of `vector<unique_ptr<Shape>>`. But because I need pointers (or references) for the next example, I am introducing them here.

If the requirement arises that another type derived from `Shape`—say, `Triangle`—is added, then you must do the following:

- Add a new entry to the `ShapeTag` enumeration.
- Make the class `Shape` fit for the size specifications of a triangle.
- Extend the distinction in `AreaCalculator::area` with a new area formula.

The open/closed solution does it better:

- The objects hide their data and know their own behavior.
- The abstract base class defines an interface against which the logic is developed.

```cpp
// https://godbolt.org/z/M6hsYa7or
#include <vector>
#include <memory>    // unique_ptr
#include <iostream>  // cout
struct Shape {
    virtual ~Shape() {}
    virtual double area() const = 0; // abstract
};
class Rectangle : public Shape {
    double w_, h_;
public:
    Rectangle(double w, double h) : w_{w}, h_{h} {}
    double area() const override { return w_ * h_; }
};
class Circle : public Shape {
    double r_;
public:
    Circle(double r) : r_{r} {}
    double area() const override { return 3.1415*r_ * r_; }
};
class AreaCalculator { // Logic
public:
    double area(const std::vector<std::unique_ptr<Shape>>& shapes) const {
        double result = 0;
        for(auto &shape : shapes) {
            result += shape->area();
        }
        return result;
    }
};
int main() {
    std::vector<std::unique_ptr<Shape>> data{};
    data.push_back(std::make_unique<Circle>(10.));        // a circle
    data.push_back(std::make_unique<Rectangle>(4., 6.));  // a rectangle
    // calculate
    AreaCalculator calc{};
    std::cout << calc.area( data ) << "\n";
}
```

**Listing 19.5** Follows the OCP.

The Shape class is the *interface* here, which the data classes then implement. Do you see that the AreaCalculator is implemented against exactly this interface? The area method does not take a bunch of Rectangles or Circles, but Shape.

An interface is characterized by the fact that it does not provide an implementation, but only describes function declarations. This is what Shape does by declaring all methods pure virtual, i.e., virtual and = 0. In other languages, this is called an abstract method. A class with at least one abstract method is called an abstract class. Abstract classes exclusively with abstract methods are called signature classes. This term is less known in other languages. In Java, such classes are called interfaces. (Java interfaces can also contain implementations with default methods, which I will ignore here.)

### Dynamic Polymorphism

> The area() method must not take Shape as a value parameter, because then the parameters would be copied according to the rules of Shape—that is, sliced, as shown in Listing 19.1. For the same reason, vector<Shape> is also not allowed, because only sliced copies would end up in it. And because Shape is an abstract class (a class with a virtual method that is = 0), the compiler would also complain.
>
> Therefore, vector stores pointers to Shape instances. To have cleanup done automatically, I use unique_ptr right away, but that's incidental. unique_ptr now allows *dynamic polymorphism*: each pointer knows whether it points to a Rectangle or a Circle. When I then call area(), the correct method is called *dynamically*—but only because the method is marked with virtual. You can read how this works in Chapter 15.

In the example, `Rectangle` and `Circle` are each derived from `Shape`. What if some of these classes have other interfaces? You can simply add these via multiple inheritance, see Chapter 18. I recommend taking Java as an example in C++ and using multiple inheritance only with signature classes; at most one ancestor should be a nonsignature class. I repeat this here because I find it so important.

> **OCP and SRP Are Closely Linked**
>
> Very often, a violation of SRP is also simultaneously associated with a violation of OCP and vice versa. Code that only requires a local change is likely to only result in the replacement of a module. A system that is cleanly divided with interfaces is also more likely to be cleanly divided by responsibilities.

## Liskov Substitution Principle

What sounds clear and logical with vehicles like `VanBus` and `Car` is often a stumbling block in practice. This is not just about type relationships, but also about their behavior. Is an overriding method allowed to throw different exceptions? What restrictions on parameters and returns are possible (e.g., is null allowed)? Does a `final` method already violate the LSP if it calls any other non-`final` method? In complicated hierarchies, one often has to ask whether the LSP is being violated. Often, the matter is not so simple, and only common sense helps.

One example, or even *the* classic example, of an LSP violation revolves around the geometric shapes of the rectangle and the square. Intuitively, one might build a class hierarchy where `Rectangle` is the base class and `Square` is the derived class, because a square *is-a* rectangle, right?

```cpp
// https://godbolt.org/z/rc67xWWFT
#include <iostream>
struct Point { int x, y; };
class Rectangle {
protected:
    Point origin_; int width_; int height_;
public:
    Rectangle(Point o, int w, int h) : origin_(o), width_(w), height_(h) {}
    virtual void setHeight(int height) { height_ = height; }
    virtual int getHeight() const { return height_; }
    virtual void setWidth(int width) { width_ = width; }
    virtual int getWidth() const { return width_; }
    virtual int getArea() const { return width_ * height_; }
};
class Square : public Rectangle {
public:
    Square(Point o, int wh) : Rectangle(o, wh, wh) {}
```

```cpp
struct Base3 {
    virtual vector<B>& func();
};
struct Derived3 : public Base3 {
    virtual vector<D>& func() override; // vector<D>& is not covariant
};
struct Base4 {
    virtual vector<B>*& func();
};
struct Derived4 : public Base4 {
    virtual vector<D>*& func() override; // different type, not covariant
};
```

**Listing 19.6** Covariance for return types.

In Derived1, C++ allows the D& return type in the overriding func() method. This is covariant to B& just as Derived1 is to Base1. If the return is a value type and not a reference like D in Derived2, then this is *not covariant* because the return would be *sliced*. This can also be applied to a vector<D>& return type: each individual value of the container would be sliced, even if the return itself is a reference.

In the Derived4 and Base4 hierarchy, vector<D>*& is also *not covariant* with vector<B>*&. In C++, these are completely different types that are not related to each other. If you encounter such a case, it is acceptable to choose vector<B>*& as the return type of the overriding method. However, note that the LSP applies not only to the type system but also to the overall behavior.

## Interface Segregation Principle

SRP is all about actors and high-level architecture. OCP deals with class design and extensibility, and LSP addresses subtypes and inheritance. ISP makes statements about the communication of components and business logic.

In all modular programs, there must be some kind of interface that users can rely on. These can be real objects that present their interface type-safely with signature classes. There are classic design patterns for this, such as facades. These are intended to regulate the user's communication with the module.

ISP is about how a module should present its interfaces to the outside.

The consideration starts with having functionality in a module that should be used by others. For example, I could identify the interface with the methods from *Figure 19.1*.

If I start this way, it will likely lead to the module being implemented in one of the following two ways:
