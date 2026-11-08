```
```cpp
int main() {
    Base2 ba2{}; output(ba2);  // outputs 8
    Value2 va2{}; output(va2); // outputs 10, because the object is not copied
}
```
```

Listing 15.12 Passing by reference does not change the instance.

When va2 becomes x, it is only “renamed.” x remains essentially a Value2—and thus print can access the virtual Value2::value method and output 10.

*Runtime polymorphism* is in play when a more general class is used in a declaration, but at runtime, a more specific class is used for the declared variable without losing its properties. In the example, although the parameter is declared as Base2, output can be called at runtime with a va2 instance of the Value2 class, and va2 retains its property of outputting 10—which it would not do if it were completely converted to the Base2 type. You achieve this form of polymorphism in C++ only when you work with references (or pointers).

In case you’re wondering, if Base2::value() were not virtual (just like Base::value()), you would be back to the behavior from Listing 15.6 and would receive an 8.

# 15.11 When to Use Virtual?

Whether you mark a method with virtual or not depends on the design you choose. In C++, it is not common practice to make all methods of all classes virtual by default. There can be reasons for and against making each individual method virtual, and the same applies to each individual class. This is somewhat different from the reasons for choosing between methods and free functions: encapsulation with methods is better, and so you usually opt for them. When it comes to deciding whether to use virtual methods or not, the matter is not quite as clear. Take the following hints as decision aids for your design:

+   - Some classes primarily serve the purpose of holding data together. They are not part of a hierarchy. Without inheritance, there is no reason for virtual methods.
+   - The existence of a class hierarchy alone does not justify virtual methods. Maybe you are just deduplicating very skillfully.
+   - Overriding a method within a class hierarchy is a good candidate for a virtual method, but not necessarily.
+   - If your design relies on overridden methods—that is, changing behavior from class to class—then virtual is appropriate.
+   - Constructors are never virtual. You must not call virtual methods within constructors.