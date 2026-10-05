# 664 Introduction to C++

```
void f(const Shape& s)
{
    s.draw();
}
```

```
int main()
{
    Circle c;
    f(c);
    return 0;
}
```

As we know, it is allowed to pass in f() a reference or pointer to a derived class object. Because draw() is virtual and s refers to what the compiler arranges for dynamic binding to the Circle::draw() function. So, the program displays Circle. To realize the strength and flexibility of the runtime polymorphism, supported by virtual functions, consider a real application which draws shapes. We can add any shape we have derived from Shape, define its own draw() and call f(). Here is the beauty; we have no need to change f(). f() has no idea what type of object is actually passed to it, though the program draw() is called. That is, we extend our program without modifying existing code. No doubt, the mechanism is a very powerful technique for implementing maintainable applications to extensions.

Note that if we pass a pointer to a Circle object, instead of the Circle, Circle::draw() function will be called again, with the necessary changes in the code of course. These examples demonstrate the flexibility of virtual functions. But, pay attention, if we pass an array, we pass a pointer as you already know, problems may arise. I will show you in an example in the last section, to something that happened to me.

If draw() was not virtual the program would display Shape. And if we change f() to accept an object, that we write:

```
void f(Shape s){s.draw()}; what will be the output?
```

Since s is an Shape object, the function Shape::draw() will be called and the program displays Shape. With this example, I want to make clear once more that when virtual functions are called by objects and not by pointers or references, there is no special treatment. That is, the function of the respect class will be called. In another example, what does the following program output?

```
int main()
{
    Shape sh;
    Circle cir;
    sh.draw();
    cir.draw();
    return 0;
}
```

In each call, the draw() function of the corresponding class is called. Thus, the program displays Shape Circle. The binding of objects (e.g., sh) to function calls, whether the functions are virtual (e.g., draw() or not, is static; it happens when the program is compiled, depending on the type of the object.

![](bbox=[0.088, 0.862, 0.145, 0.902])

The different behaviour of virtual functions happens at runtime when they are called through references or pointers to objects of derived classes and not called from the objects themselves. When an object is used to call a virtual function, the call is resolved statically at compile time.