its base class. If we do not declare the base-class function as `virtual`, we can redefine that function. By contrast, if we declare the base-class function as `virtual`, we can override that function to enable polymorphic behavior. We declare a virtual function by preceding the function’s prototype with the keyword `virtual` in the base class. For example,

```
virtual void draw() const;
```

would appear in base class Shape. The preceding prototype declares that function draw is a virtual function that takes no arguments and returns nothing. This function is declared const because a draw function typically would not make changes to the Shape object on which it’s invoked—virtual functions do not have to be const functions.

![](bbox=[0.159, 0.296, 0.216, 0.344])

> **Software Engineering Observation 13.4**
> 
> *Once a function is declared virtual, it remains virtual all the way down the inheritance hierarchy from that point, even if that function is not explicitly declared virtual when a derived class overrides it.*

![](bbox=[0.159, 0.381, 0.216, 0.425])

> **Good Programming Practice 13.1**
> 
> *Even though certain functions are implicitly virtual because of a declaration made higher in the class hierarchy, explicitly declare the functions virtual at every level of the hierarchy to promote program clarity.*

![](bbox=[0.159, 0.472, 0.216, 0.523])

> **Error-Prevention Tip 13.1**
> 
> *When you browse a class hierarchy to locate a class to reuse, it’s possible that a function in that class will exhibit virtual function behavior even though it’s not explicitly declared virtual. This happens when the class inherits a virtual function from its base class, and it can lead to subtle logic errors. Such errors can be avoided by explicitly declaring all virtual functions virtual throughout the inheritance hierarchy.*

![](bbox=[0.159, 0.588, 0.216, 0.634])

> **Software Engineering Observation 13.5**
> 
> *When a derived class chooses not to override a virtual function from its base class, the derived class simply inherits its base class’ virtual function implementation.*

If a program invokes a virtual function through a base-class pointer to a derived-class object (e.g., `shapePtr->draw()`) or a base-class reference to a derived-class object (e.g., `shapeRef.draw()`), the program will choose the correct derived-class draw function dynamically (i.e., at execution time) based on the object type—not the pointer or reference type. Choosing the appropriate function to call at execution time (rather than at compile time) is known as dynamic binding or late binding.

When a virtual function is called by referencing a specific object by name and using the dot member-selection operator (e.g., `squareObject.draw()`), the function invocation is resolved at compile time (this is called static binding) and the virtual function that is called is the one defined for (or inherited by) the class of that particular object—this is not polymorphic behavior. Thus, dynamic binding with virtual functions occurs only off pointer (and, as we’ll soon see, reference) handles.

Now let’s see how virtual functions can enable polymorphic behavior in our employee hierarchy. Figures 13.8–13.9 are the header files for classes CommissionEmployee and BasePlusCommissionEmployee, respectively. The only difference between these files and those of Fig. 13.1 and Fig. 13.3 is that we specify each class’s earnings and