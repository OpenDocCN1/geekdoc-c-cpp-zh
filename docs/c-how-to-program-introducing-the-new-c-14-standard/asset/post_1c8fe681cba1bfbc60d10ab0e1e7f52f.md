
The compiler will allow access to derived-class-only members from a base-class pointer that’s aimed at a derived-class object **if** we explicitly cast the base-class pointer to a derived-class pointer—this is known as **downcasting**. As you know, it’s possible to aim a base-class pointer at a derived-class object. However, as we demonstrated in **Fig. 12.3**, a base-class pointer can be used to invoke *only* the functions declared in the base class. Downcasting allows a derived-class-specific operation on a derived-class object pointed to by a base-class pointer. Downcasting is a potentially *dangerous* operation. **Section 12.9** demonstrates how to *safely* use downcasting.

## 12.4 Virtual Functions and Virtual Destructors

In **Section 12.3.1**, we aimed a base-class `CommissionEmployee` pointer at a derived-class `BasePlusCommissionEmployee` object, then invoked member function `toString` through that pointer. Recall that the *type of the handle* determined which class’s functionality to invoke. In that case, the `CommissionEmployee` pointer invoked the `CommissionEmployee` member function `toString` on the `BasePlusCommissionEmployee` object, even though the pointer was aimed at a `BasePlusCommissionEmployee` object that has its own custom `toString` function.

### 12.4.1 Why `virtual` Functions Are Useful

Suppose that shape classes such as `Circle`, `Triangle`, `Rectangle` and `Square` are all derived from base class `Shape`. Each of these classes might be endowed with the ability to *draw itself* via a member function `draw`, but the function for each shape is quite different. In a program that draws a set of shapes, it would be useful to be able to treat all the shapes *generally* as objects of the base class `Shape`. Then, to draw any shape, we could simply use a base-class `Shape` pointer to invoke function `draw` and let the program determine *dynamically* (i.e., at runtime) which derived-class `draw` function to use, based on the type of the object to which the base-class `Shape` pointer points at any given time. This is *polymorphic behavior*.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1563_0.png)

### Software Engineering Observation 12.3

*With* `virtual` *functions, the type of the object—not the type of the handle used to invoke the object’s member function—determines which version of a* `virtual` *function to invoke.*

### 12.4.2 Declaring `virtual` Functions

To enable this behavior, we declare `draw` in the base class as a **virtual function**, and we **override** `draw` in *each* of the derived classes to draw the appropriate shape. From an implementation perspective, *overriding* a function is no different than *redefining* one (which is the approach we’ve been using until now). An overridden function in a derived class has the *same signature and return type* (i.e., *prototype*) as the function it overrides in its base class. If we *do not* declare the base-class function as `virtual`, we can *redefine* that function.

By contrast, if we *do* declare the base-class function as `virtual`, we can *override* that function to enable *polymorphic behavior*. We declare a `virtual` function by preceding the function’s prototype with the keyword `virtual` in the base class. For example,

```cpp
virtual void draw() const;
```

would appear in base class `Shape`. The preceding prototype declares that function `draw` is a `virtual` function that takes no arguments and returns nothing. This function is declared `const` because a `draw` function typically would not make changes to the `Shape` object on which it’s invoked. Virtual functions do *not* have to be `const` functions.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1565_0.png)

### Software Engineering Observation 12.4

Once a function is declared `virtual`, it remains `virtual` all the way down the inheritance hierarchy from that point, even if that function is not explicitly declared `virtual` when a derived class overrides it.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1565_1.png)

### Good Programming Practice 12.1

Even though certain functions are implicitly `virtual` because of a declaration made higher in the class hierarchy, for clarity explicitly declare these functions `virtual` at every level of the class hierarchy.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1565_2.png)

### Software Engineering Observation 12.5

When a derived class chooses not to override a `virtual` function from its base class, the derived class simply inherits its base class’s `virtual` function implementation.

### 12.4.3 Invoking a `virtual` Function Through a Base-Class Pointer or Reference

If a program invokes a `virtual` function through a base-class pointer to a derived-class object (e.g., `shapePtr->draw()`) or a base-class reference to a derived-class object (e.g., `shapeRef.draw()`), the program will choose the correct derived-class function *dynamically* (i.e., at execution time) *based on the object type—not the pointer or reference type*. Choosing the appropriate function to call at execution time (rather than at compile time) is known as **dynamic binding**.

### 12.4.4 Invoking a `virtual` Function Through an Object’s Name

When a `virtual` function is called by referencing a specific object by *name* and using the dot member-selection operator (e.g., `squareObject.draw()`), the function invocation is *resolved at compile time* (this is called **static binding**) and the `virtual` function that’s called is the one defined for (or inherited by) the class of that particular object—this is *not* polymorphic behavior. Dynamic binding with `virtual` functions occurs only off pointers and references.

### 12.4.5 `virtual` Functions in the `CommissionEmployee` Hierarchy

Now let’s see how `virtual` functions can enable polymorphic behavior in our employee hierarchy. **Figures 12.4–12.5** are the headers for classes `CommissionEmployee` and `BasePlusCommissionEmployee`, respectively. We’ve modified these to declare each class’s `earnings` and `toString` member functions as `virtual` (lines 28–29 of **Fig. 12.4** and lines 17–18 of **Fig. 12.5**). Because functions `earnings` and `toString` are `virtual` in class `CommissionEmployee`, class `BasePlusCommissionEmployee`’s `earnings` and `toString` functions **override** class `CommissionEmployee`’s. In addition, class `BasePlusCommissionEmployee`’s `earnings` and `toString` functions are declared with C++11’s **override** keyword.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1569_0.png)

### Error-Prevention Tip 12.1

*To help prevent errors, apply C++11’s `override` keyword to the prototype of every derived-class function that overrides a base-class `virtual` function. This enables the compiler to check whether the base class has a `virtual` member function with the same signature. If not, the compiler generates an error. Not only does this ensure that you override the base-class function with the appropriate signature, it also prevents you from accidentally hiding a base-class function that has the same name and a different signature.*

Now, if we aim a base-class `CommissionEmployee` pointer at a derived-class `BasePlusCommissionEmployee` object, and the program uses that pointer to call either function `earnings` or `toString`, the `BasePlusCommissionEmployee` object’s corresponding function will be invoked *polymorphically*. There were no changes to the member-function implementations of classes `CommissionEmployee` and `BasePlusCommissionEmployee`, so we reuse the versions of **Figs. 11.14** and **11.15**.

```cpp
// Fig. 12.4: CommissionEmployee.h
// CommissionEmployee class with virtual earnings and toString functions.
#ifndef COMMISSION_H
#define COMMISSION_H

#include <string> // C++ standard string class

class CommissionEmployee {
public:
    CommissionEmployee(const std::string& first, const std::string&,
        const std::string& ssn, double = 0.0, double = 0.0);

    void setFirstName(const std::string&); // set first name
    std::string getFirstName() const; // return first name

    void setLastName(const std::string&); // set last name
    std::string getLastName() const; // return last name

    void setSocialSecurityNumber(const std::string&); // set SSN
    std::string getSocialSecurityNumber() const; // return SSN

    void setGrossSales(double); // set gross sales amount
    double getGrossSales() const; // return gross sales amount

    void setCommissionRate(double); // set commission rate (percentage)
    double getCommissionRate() const; // return commission rate

    virtual double earnings() const; // calculate earnings
    virtual std::string toString() const; // string representation
private:
    std::string firstName;
    std::string lastName;
    std::string socialSecurityNumber;
    double grossSales; // gross weekly sales
    double commissionRate; // commission percentage
};

#endif
```

**Fig. 12.4** `CommissionEmployee` class header declares `earnings` and `toString` as `virtual`.
