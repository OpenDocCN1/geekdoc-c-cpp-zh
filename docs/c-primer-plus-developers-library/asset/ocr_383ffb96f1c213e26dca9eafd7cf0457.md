```
```cpp
{
    DR o1;          // use DR()
    DR o2(18.81);   // use DR(double) instead of BS(double)
    DR o3(10.1, 8); // use BS(int, double)
    ...
}
```
```

Because there is no `DR(int, double)` constructor, the inherited `BS(int, double)` is used for o3. Note that an inherited base-class constructor only initializes base-class members. If you need to initialize derived class members too, you can use the member list initialization syntax used in the inheritance:

```
```cpp
DR(int i, int k, double x) : j(i), BS(k, x) {}
```
```

# Managing Virtual Methods: override and final

Virtual methods are an important component of implementing polymorphic class hierarchies, in which a base class reference or pointer can invoke the particular method appropriate to the type of object referred to. Virtual methods do pose some programming pitfalls. For instance, suppose the base class declares a particular virtual method, and you decide to provide a different version for a derived class. This is called *overriding* the old version. But, as discussed in Chapter 13, “Class Inheritance,” if you mismatch the function signature, you hide rather than override the old version:

```
```cpp
class Action
{
    int a;
public:
    Action(int i = 0) : a(i) {}
    int val() const { return a;}
    virtual void f(char ch) const { std::cout << val() << ch << "\n";}
};
class Bingo : public Action
{
public:
    Bingo(int i = 0) : Action(i) {}
    virtual void f(char * ch) const { std::cout << val() << ch << "!\n"; }
};
```
```

Because class Bingo uses `f(char * ch)` instead of `f(char ch)`, `f(char ch)` is hidden to a Bingo object. This prevents a program from using code like the following:

```
```cpp
Bingo b(10);
b.f('g');  // works for Action object, fails for Bingo object
```
```

With C++11, you can use the virtual specifier `override` to indicate that you intend to override a virtual function. Place it after the parameter list. If your declaration does not match a base method, the compiler objects. Thus, the following version of Bingo::f() would generate a compile-time error message: