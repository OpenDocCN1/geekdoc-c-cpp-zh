The `nullsFirst` method needs a comparator—in this case, one that compares two strings. The `naturalOrder` method makes a comparator for any class implementing `Comparable`. A `Comparator<String> naturalOrder()` is what we need. Here is the complete call for sorting by potentially null middle names. I use a static import of `java.util.Comparator.*`, to make the expression more legible. Note that the type for `naturalOrder` is inferred.

```
```java
Arrays.sort(people, comparing(Person::getMiddleName,
    nullsFirst(naturalOrder())));
```
```

The static `reverseOrder` method gives the reverse of the natural order. To reverse any comparator, use the reversed instance method. For example, `naturalOrder().reversed()` is the same as `reverseOrder()`.

# 6.3 Inner Classes

An *inner class* is a class that is defined inside another class. Why would you want to do that? There are two reasons:

+   - Inner classes can be hidden from other classes in the same package.
+   - Inner class methods can access the data from the scope in which they are defined—including the data that would otherwise be private.

Inner classes used to be very important for concisely implementing callbacks, but nowadays lambda expressions do a much better job. Still, inner classes can be very useful for structuring your code. The following sections walk you through all the details.

![](bbox=[0.128, 0.733, 0.18, 0.773])

# C++ NOTE:

C++ has *nested classes*. A nested class is contained inside the scope of the enclosing class. Here is a typical example: A linked list class defines a class to hold the links, and a class to define an iterator position.