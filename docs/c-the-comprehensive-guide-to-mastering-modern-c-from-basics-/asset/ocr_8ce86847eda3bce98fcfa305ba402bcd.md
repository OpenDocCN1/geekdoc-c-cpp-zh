Value2 v2{}; v2.print(cout); corresponds to the Value v{}; v.print(cout); call from the previous listing. Now you will see 10, v2.print() must refer to the Base2::print definition because Value2 has not defined this method itself, the call to value() in print is now a virtual method call: it is decided at runtime. And because v2 is of type Value2, Value2::value is used, ten_ is returned, and thus 10 is output.

# Virtual and Nonvirtual

Virtual method calls are decided at runtime, normal method calls at compile time.

In Listing 15.7, in the definition of the value() method, you see the override keyword in addition to the virtual keyword. Such an additional designation requires the compiler to ensure that this method overrides another method. This way, you can avoid producing hard-to-find errors due to a typo, for example. Imagine, for instance, that you accidentally named the method virtual int value() const in Value2. The program will compile and run, but it will not return the values you expect.

Or consider this other, quite practical example. In mydefs.hpp header file, some types are defined, such as using value_t = int. And now you have a small hierarchy:

```
struct Number {
  virtual void add(value_t value);
};
struct SafeName : public Number {
  virtual void add(int value); // override not specified, int instead
```