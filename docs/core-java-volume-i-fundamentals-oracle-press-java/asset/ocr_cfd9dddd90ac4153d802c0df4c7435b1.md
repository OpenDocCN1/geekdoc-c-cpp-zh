```
```java
List<String> safeStrings = Collections.checkedList(strings,
String.class);
```
```

The view’s `add` method checks that the inserted object belongs to the given class and immediately throws a `ClassCastException` if it does not. The advantage is that the error is reported at the correct location:

```
```java
ArrayList rawList = safeStrings;
rawList.add(new Date()); // checked list throws a
ClassCastException
```
```

![](bbox=[0.128, 0.374, 0.181, 0.414])

> > **CAUTION:**
> >
> > The checked views are limited by the runtime checks that the virtual machine can carry out. For example, if you have an `ArrayList<Pair<String>>`, you cannot protect it from inserting a `Pair<Date>` since the virtual machine has a single “raw” `Pair` class.

# 9.5.5 Synchronized Views

If you access a collection from multiple threads, you need to ensure that the collection is not accidentally damaged. For example, it would be disastrous if one thread tried to add to a hash table while another thread was rehashing the elements.

Instead of implementing thread-safe collection classes, the library designers used the view mechanism to make regular collections thread-safe. For example, the static `synchronizedMap` method in the `Collections` class can turn any map into a map with synchronized access methods:

```
```java
var map = Collections.synchronizedMap(new HashMap<String,
Employee>());
```
```