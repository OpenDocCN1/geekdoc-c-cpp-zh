# Radio

Here, a Radio object has two subobjects of class Component. Consequently, a dynamic_cast from Storable to Component within a Radio will be ambiguous and return a 0. There is simply no way of knowing which Component the programmer wanted:

```
void h1(Radio& r)
{
Storable* ps = &r; // aRadio has a unique Storable
//...
Component* pc = dynamic_cast<Component*>(ps); // pc = 0; a Radio has twoComponents //...
}
```

In general – and typically – a programmer (and a compiler looking at a single translation unit) does not know the complete class lattice. Instead, code is written with the knowledge of some sublattice. For example, a programmer might know only about the Transmitter part of a Radio and write:

```
void h2(Storable*ps) // ps might or might not point to a Component
{
if (Component* pc = dynamic_cast<Component*>(ps)) {
// wehaveacomponent!
}
else {
// it wasn’t a Component
}
}
```

The ambiguity for a pointer to a Radio object is not in general detectable at compile time. This kind of run-time ambiguity detection is needed only for virtual bases. For ordinary bases, there is always a unique subobject of a given cast (or none) when downcasting (that is, toward a derived class; §22.2). The equivalent ambiguity for virtual bases occurs when upcasting (that is, toward a base), but such ambiguities are caught at compile time.

# 22.2.3 static_cast and dynamic_cast

A dynamic_cast can cast from a polymorphic virtual base class to a derived class or a sibling class (§22.2.1). A static_cast (§11.5.2) does not examine the object it casts from, so it cannot:

```
void g(Radio& r)
{
Receiver* prec = &r; // Receiver is an ordinarybase of Radio Radio* pr =
static_cast<Radio*>(prec); // OK, unchecked
pr = dynamic_cast<Radio*>(prec); // OK, run-time checked
Storable * ps = &r; // Storable is a virtual base of Radio
```