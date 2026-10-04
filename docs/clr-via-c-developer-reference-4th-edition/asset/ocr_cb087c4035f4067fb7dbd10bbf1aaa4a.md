```
public Int32 CompareTo(SomeValueType other) {
    return(m_x - other.m_x);
}
```

```
// NOTE: like public/private used on the next line
Int32 IComparable.CompareTo(Object other) {
    return CompareTo(SomeValueType) other);
}
```

Notice changes in this new version. First it now has two CompareTo methods. The first CompareTo method no longer takes an Object as a parameter; it now takes a SomeValueType instead. Because this parameter has changed, the code that casts other to SomeValueType is no longer necessary and has been removed. Changing, the first CompareTo method to make type-safe means that SomeValueType no longer adheres to the contract placed on it implementing the IComparable interface. So SomeValueType must implement a CompareTo method that satisfies the IComparable contract. This is the job of the second IComparable.CompareTo method, which is an EMI.

Having made these two changes means that we get compile-time type safety and no boxing.

```
public static void Main() {
    SomeValueType v = new SomeValueType();
    Object o = new Object();
    Int32 n = v.CompareTo(v); // No boxing
    n = v.CompareTo(o); // compile-time error
}
```

If, however, we define a variable of the interface type, we will lose compile-time type safety and experience undesired boxing again.

```
public static void Main() {
    SomeValueType v = new SomeValueType();
    IComparable c = v; // Boxing!

    Object o = new Object();
    Int32 n = c.CompareTo(v); // Undesired boxing
    n = c.CompareTo(o); // InvalidCastException
}
```

In fact, as mentioned earlier in this chapter, when casting a value type instance to an interface type, the CLR must box the value type instance. Because of this fact, two boxing occur in the previous Main method.

EMIs are frequently used when implementing interfaces as IConvertible, ICollection, IList, and IDictionary. They let you create type-safe versions of these interfaces' methods, and they enable you to reduce boxing operations for value types.