# Chapter 12 Support for Object-Oriented Programming

```
ptr_shape = sq; // Now ptr_shape points to a
// Square object
ptr_shape->draw(); // Dynamically bound to the draw
// in the Square class
rect->draw(); // Statically bound to the draw
// in the Rectangle class
```

This situation is shown in Figure 12.6.

Notice that the draw function in the definition of the base class shape is set to 0. This peculiar syntax is used to indicate that this member function is a pure virtual function, meaning that it has no body and it cannot be called. It must be redefined in derived classes if they call the function. The purpose of a pure virtual function is to provide the interface of a function without giving any of its implementation. Pure virtual functions are usually defined when an actual member

![](bbox=[0.05, 0.52, 0.95, 0.82])

| Types | Pointers | Bindings | Objects |
|-------|----------|----------|---------|
| Shape* | ptr_shape | → Square | Square |
| Square* | sq | → Square | Square |
| Rectangle* | rect | → Rectangle | Rectangle |