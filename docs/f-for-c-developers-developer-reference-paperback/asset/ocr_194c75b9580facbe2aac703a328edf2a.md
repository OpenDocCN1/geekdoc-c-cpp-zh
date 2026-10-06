# LISTING 2-41 Upcasting conversion

```
// define a base class
type Base() = class end

// define a derived class
type Derived() = inherit Base()

let myDerived = Derived()

// upcasting
let cast = myDerived <: Base

// use upcast
let cast2 : Base = upcast myDerived
```

**Note** Casting to a base class (using -> or upcast) is always safe and can be verified at compile time.

Casting an object down the hierarchy happens when you need to cast from a base object to a derived object. The -> operator or the downcast keyword is used to accomplish this. The downcast operator does some sanity checks; for example, the type casting needs to have an inheritance relationship with current type, but most of the checking still has to be verified at runtime. If the cast fails, an InvalidCastException will be raised. Listing 2-42 casts the base class to a derived class.

# **LISTING 2-42** example of downcasting

```
// define a base class
type Base() = class end

// define a derived class
type Derived() = inherit Base()

let myDerived = Derived()

// upcasting
let upcastResult = myDerived <: Base

// use upcast
let cast2 : Base = upcast myDerived

// downcasting
let downcastResult = upcastResult :> Derived

// use downcast
let case3 : Derived = downcast cast
```