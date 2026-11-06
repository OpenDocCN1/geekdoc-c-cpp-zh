# # 14.5 Virtual functions and multiple inheritance

In chapter 6 we encountered the class `fstream`, one class offering features of `ifstream` and `ofstream`. In chapter 13 we learned that a class may be derived from multiple base classes. Such a derived class inherits the properties of all its base classes. Polymorphism can also be used in combination with multiple inheritance.

Consider what would happen if more than one ‘path’ leads from the derived class up to its (base) classes. This is illustrated in the next (fictitious) example where a class `Derived` is doubly derived from `Base`:

```
```cpp
class Base
{
    int d_field;
    public:
        void setfield(int val);
        int field() const;
};
inline void Base::setfield(int val)
{
    d_field = val;
}
inline int Base::field() const
{
    return d_field;
}

class Derived: public Base, public Base
{
};
```
```

Due to the double derivation, `Base`'s functionality now occurs twice in `Derived`. This results in ambiguity: when the function `setfield()` is called for a `Derived` class object, which function will that be as there are two of them? The scope resolution operator won't come to the rescue and so the C++ compiler cannot compile the above example and (correctly) identifies an error.

The above code clearly duplicates its base class in the derivation, which can of course easily be avoided by not doubly deriving from `Base` (or by using composition (!)). But duplication of a base class can also occur through nested inheritance, where an object is derived from, e.g., an `Auto` and from an `Air` (cf. section 13.1). Such a class would be needed to represent, e.g., a flying car³. An `AirAuto` would ultimately contain two `Vehicles`, and hence two `mass` fields, two `setMass()` functions and two `mass()` functions. Is this what we want?

# ## 14.5.1 Ambiguity in multiple inheritance

Let's investigate closer why an `AirAuto` introduces ambiguity, when derived from `Auto` and `Air`.

+   - An `AirAuto` is an `Auto`, hence a `Land`, and hence a `Vehicle`.
+   - However, an `AirAuto` is also an `Air`, and hence a `Vehicle`.

The duplication of `Vehicle` data is further illustrated in Figure 14.1. The internal organization of an `AirAuto` is shown in Figure 14.2 The C++ compiler detects the ambiguity in an `AirAuto` object, and will therefore not compile statements like:

```
```cpp
AirAuto jBond;
cout << jBond.mass() << '\n';
```
```

²such as the one in James Bond vs. the Man with the Golden Gun...