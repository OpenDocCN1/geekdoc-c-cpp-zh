(iii) You must provide the new implementation that overrides the default behaviour.

Here is an example for the **PutOption** class.

```
`class PutOption : public ContinuousTimeOptionBase { public: double price(const BlackScholesModel& bsm) const override; // ... other members ... };`
```

This means that the **PutOption** has a different price function than the default one. The implementation of this method is just the usual Black–Scholes pricing formula that we’ve seen before.

The `override` keyword does not affect the behaviour of the program when it is running. It is simply a way of saying that your intention is to override a function. If you do not use this keyword and you make a small error in the list of parameter types of your function then the compiler may not notice your error. This can lead to bugs that are hard to spot. Therefore it is advisable to use `override` whenever you wish to override a function.

When you call `price` on an option, the appropriate `price` method will be automatically selected based on the type of the option. This will allow us to write a class that prices an entire Portfolio of options in the next chapter.

# ### 12.4.1 A note on the keyword virtual

The keyword `virtual` means “may be overridden”.

When you write an interface class, the methods have no definitions, so we must always declare them as virtual because they *must* be overridden.

All classes have a destructor. This is a special function called when the object is destroyed. This must be declared as `virtual` in any class that may be subclassed so that the overridden destructor will be called.

This explains why we had to use the keyword `virtual` several times in the definition of an interface class.

# #### **Danger!**

**Virtual destructors:** any class that is designed to be subclassed should have a virtual destructor. Unfortunately most compilers don’t pick up on it if you forget to write one.