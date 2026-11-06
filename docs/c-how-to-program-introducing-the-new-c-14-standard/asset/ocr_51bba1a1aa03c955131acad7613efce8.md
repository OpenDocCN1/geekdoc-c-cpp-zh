# 12.4.2 Declaring `virtual`
Functions

To enable this behavior, we declare `draw` in the base class as a **virtual function**, and we **override** `draw` in *each* of the derived classes to draw the appropriate shape. From an implementation perspective, *overriding* a function is no different than *redefining* one (which is the approach we’ve been using until now). An overridden function in a derived class has the *same signature and return type* (i.e., *prototype*) as the function it overrides in its base class. If we *do not* declare the base-class function as `virtual`, we can *redefine* that function.

By contrast, if we *do* declare the base-class function as `virtual`, we can *override* that function to enable *polymorphic behavior*. We declare a `virtual` function by preceding the function’s prototype with the keyword `virtual` in the base class. For example,

```
```cpp
virtual void draw() const;
```
```

would appear in base class `Shape`. The preceding prototype declares that function `draw` is a `virtual` function that takes no arguments and