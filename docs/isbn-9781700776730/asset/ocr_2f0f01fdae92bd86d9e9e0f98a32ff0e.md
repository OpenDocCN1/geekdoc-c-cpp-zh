```
class base {
  public:
    int num;
};
class X : public virtual Base { };
class Y : public virtual Base { };
class Z : public X, public Y {
  public:
    int getNum() { return num; }
};
```

Note that we no longer need to use the scope resolution operator in the return statement of the getNum() member function in class Z. Base is now a virtual base class and class Z only has one object of class Base.

![](bbox=[0.178, 0.452, 0.622, 0.715])

Note that virtual base classes are used only in the context of multiple inheritance and have nothing to do with abstract base classes (which contain a pure virtual function).