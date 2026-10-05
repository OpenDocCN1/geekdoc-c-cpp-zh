# 658 Introduction to C++

Let's discuss now virtual functions and one of the most important features of C++, the dynamic or runtime polymorphism. If we declare show() as virtual in the base class, the results are different. To declare it as virtual we use the keyword virtual. For example:

```
class Product
{
    virtual void show() const;
};

class Book : public Product
{
    virtual void show() const;
};
```

![](bbox=[0.088, 0.353, 0.145, 0.381])

In order for the virtual mechanism to work, the function of the derived class must override the function of the base class.

When a function in a derived class redefines a virtual function of the base class with the same signature, it is called function overriding. Regarding the type, in general, the return type of the virtual function in the derived class should be the same as that of the base class, as well. Strictly speaking, and without getting into details, it should be covariant with the classes of the function. For example, if the return type of the base class is a pointer or a reference to a class type, the virtual function in the derived class may return a pointer or a reference to a more specialized type than that of the base. If the signatures are the same but the return types are not consistent, the derived class function won't compile.

Notice that the signatures do not match exactly, the derived class does not override the function of the base class, but it is a new function which hides one of the base class, as we saw in the previous section. For example, if you use different parameters for the function of the derived class or use different const specifier, then the function of the derived class will not be virtual, which means that the virtual mechanism won't work. We'll discuss this situation later when we meet the override

Here is the key to runtime polymorphism. When a virtual function is called by a reference or pointer, the selection of the function to be executed is based on the object to which the reference refers or to the pointer points. Therefore, the previous code displays:

```
C:A      P:1;
T:Nice   A:Many;
T:Nice   A:Many;
```

That is, we can declare a reference or pointer to a base class object, and if it refers to a derived object, the function of the derived object is called, provided that it is virtual. For example, consider a hierarchy of classes derived from the Shape class contains a virtual function named draw(). It'd be nice if we declare a reference or pointer to Shape and be able to call the draw() of each class. We can do that to the really great concept of virtual functions.

To explain the mechanism of virtual functions, we should first discuss the static and dynamic types of a pointer variable. Each pointer has a static type, which is the type of its declaration, and a dynamic type, which is the type of the object it points to. These types may also be different. For example, the static type of ptr2 is Product*, while its dynamic type is Book*. The static type is always the same, while the dynamic type can change if, for example, we change the pointer to