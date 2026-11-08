```
```cpp
std::ostream& print(std::ostream& os) const { return os << value_; }
friend class Mechanic;
};
class Mechanic {
    const Thing &thing_;
public:
    explicit Mechanic(const Thing &thing) : thing_{thing} {}
    auto getThingValue() const {
        return thing_.value_;             // access to private member of Thing
    }
};
int main() {
    Thing thing{45};
    thing.print(std::cout) << '\n';               // output: 45
    Mechanic mechanic{thing};
    thing.increment();                            // change internal value
    std::cout << mechanic.getThingValue() << '\n'; // output: 46
}
```
```

Listing 18.1 With “friend”, you can allow another class access to private members.

Normally, the Mechanic class would not be allowed access via thing.value_. However, because the Thing class considers the Mechanic class a “good friend” with the friend class Mechanic line, it is allowed to do so.

That’s basically all there is to it. There are just a few more details to consider:

+   - **The friend class must be known**
+     To write friend class Mechanic, the name Mechanic must be known beforehand. For this, it is usually necessary to declare the class once with class Mechanic. This would not be necessary if the entire definition of Mechanic had already been provided upfront, but typically this is not the case.
+   - **Friendship applies only directly**
+     Friendship is not inherited. A class derived from Mechanic does *not* get special access to Thing.

And because friendship must be declared *within* the Thing class, no one from outside who does not have direct access to the Thing class can gain the special privileges of a friend class.

This fact, combined with the noninheritance of friendship, reveals one of the biggest weaknesses of this method of granting extended rights: in larger inheritance hierarchies, multiple friend classes would need to be declared. This, in turn, breaks the actual principle of encapsulation. The friend class already does this as it is. You should carefully consider whether your design is correct if you are tempted to use friend class.