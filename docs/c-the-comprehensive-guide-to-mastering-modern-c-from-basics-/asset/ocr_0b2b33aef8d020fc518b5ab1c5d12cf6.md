```
virtual void user() override { provider(); };
};
struct Derived2 : public virtual Base { // still abstract
virtual void provider() override { cout << "Derived2::provider!\n"; };
struct DerivedDerivedDerived : public Derived1, public Derived2 { // concrete
};

int main() {
DerivedDerived dd;
DerivedDerived *pdd = &dd;
Derived1* p1 = pdd; // Cast within the hierarchy
Derived2* p2 = pdd; // Cast within the hierarchy
pdd->user(); // Output: Derived2::provider()
p1->user(); // Output: Derived2::provider()
p2->user(); // Output: Derived2::provider()
}
```

# Listing 18.19

The Base base class defines an interface here. It is abstract because it defines abstract methods—that is, defined as purely virtual with = 0 instead of a function body. The two Derived1 and Derived2 classes each implement a part of this interface, but both are still abstract. Only when combined in DerivedDerived does the class become concrete, no longer abstract, because all methods are now defined.

Interestingly, in Derived1, in user(), the call to provider() results in a method being called that is actually defined only after the combination—and this by a class that is not directly connected to the inheritance hierarchy. This is called delegating to a sister class. This technique can be a powerful tool if you want to retroactively adjust the behavior of polymorphic classes.