# ## Checkpoint

+   1. *(True/False)* A base class exists in a hierarchical relationship with its derived classes. Once classes are employed in inheritance hierarchies, they become coupled with other classes. A class can be a base class that supplies members to other classes, a derived class that inherits members from other classes or both.
+      Answer: True.
+   2. *(Fill-in)* With ______, a derived class inherits from one base class. With ______, a derived class inherits from two or more base classes.
+      Answer: single inheritance, multiple inheritance.
+   3. *(Fill-in)* A(n) ______ base class is two or more levels up the class hierarchy from its derived classes.
+      Answer: indirect.

# ## 10.2.2 Shape Class Hierarchy and public Inheritance

Let's consider a Shape inheritance hierarchy:

![](bbox=[0.2, 0.41, 0.86, 0.51])

Classes TwoDimensionalShape and ThreeDimensionalShape derive from base class Shape, so a TwoDimensionalShape is a Shape, and a ThreeDimensionalShape is a Shape. The hierarchy's third level contains specific TwoDimensionalShapes and ThreeDimensionalShapes. We can follow the arrows upward to identify direct and indirect is-a relationships. For instance, a Triangle is a TwoDimensionalShape and is a Shape, while a Sphere is a ThreeDimensionalShape and is a Shape.

The following class header specifies that TwoDimensionalShape inherits from Shape:

```
class TwoDimensionalShape : public Shape
```

This is **public inheritance**, which we'll use in this chapter. In public inheritance, **public** base-class members become **public** derived-class members and **protected** base-class members become **protected** derived-class members.<sup>4</sup> Although private base-class members are not directly accessible in derived classes, these members are still inherited and part of the derived-class objects. The derived class can manipulate private base-class members through inherited base-class **public** and **protected** member functions—if they provide such functionality. We'll discuss private and protected inheritance in Chapter 20, Other Topics and a Look Toward the Future of C++.

Inheritance is not appropriate for every class relationship. Composition's *has-a* relationship sometimes is more appropriate. For example, given *Employee*, *BirthDate* and *PhoneNumber* classes, it's improper to say that an *Employee* is a *BirthDate* or that an