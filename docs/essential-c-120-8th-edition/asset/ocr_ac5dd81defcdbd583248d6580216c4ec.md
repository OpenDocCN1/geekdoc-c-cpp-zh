# Chapter 12: Generics

Listing 12.35: Defining Generic Methods

```
public static class MathEx {
    public static T Max<T>(T first, params T[] values)
    where T : Comparable<T> {
        T maximum = first;
        foreach(T item in values) {
            if(item.compareTo(maximum) > 0) {
                maximum = item;
            }
        }
        return maximum;
    }

    public static T Min<T>(T first, params T[] values)
    where T : Comparable<T> {
        T minimum = first;
        foreach(T item in values) {
            if(item.compareTo(minimum) < 0) {
                minimum = item;
            }
        }
        return minimum;
    }
}
```

Generic methods, like generic types, can include more than one type parameter. The arity (the number of type parameters) is an additional distinguishing characteristic of a method signature. That is, it is legal to have two methods with identical names and formal parameter types, as long as they differ in method type arity.