# Solutions to Chapter 13 | C++

13.6 What is name hiding in C++ pg 76

# SOLUTION

Let us explain through an example. In C++, when you have a class with an overloaded method, and you then extend and override that method, you must override all of the overloaded methods.

For example:

```
class FirstClass {
public:
    virtual void MethodA (int);
    virtual void MethodA (int, int);
};
void FirstClass::MethodA (int i) {
    std::cout << "ONE!!\n";
}
```

This is a simple class with two methods (or one overloaded method). If you want to override the one-parameter version, you can do the following:

```
class SecondClass : public FirstClass {
public:
    void MethodA (int);
};
void SecondClass::MethodA (int i) {
    std::cout << "THREE!!\n";
}
void main () {
    SecondClass a;
    a.MethodA (1);
    a.MethodA (1, 1);
}
```

However, the second call will not work, since the two-parameter MethodA is not visible. That is name hiding.