# 9.5.2 Unmodifiable Copies and Views

To make an *unmodifiable copy* of a collection, use the `copyOf` method of the collection type:

```
```java
ArrayList<String> names = . . .;
Set<String> nameSet = Set.copyOf(names); // The names as an
unmodifiable set
List<String> nameList = List.copyOf(names); // The names as an
unmodifiable list
```
```

Each `copyOf` method makes a copy of the collection. If the original collection is modified, the copy is not affected.

If the original collection happens to be unmodifiable and of the correct type, then `copyOf` simply returns it:

```
```java
Set<String> names = Set.of("Peter", "Paul", "Mary");
Set<String> nameSet = Set.copyOf(names); // No need to make a
copy: names == nameSet
```
```

The `Collections` class has methods that produce *unmodifiable views* of collections. These views add a runtime check to an existing collection. If an attempt to modify the unmodifiable collection is detected, an exception is thrown.

However, if the original collection changes, the view reflects those changes. That is what makes views different from copies.

You obtain unmodifiable views by eight methods:

```
```java
Collections.unmodifiableCollection
Collections.unmodifiableList Collections.unmodifiableSet
Collections.unmodifiableSortedSet
Collections.unmodifiableNavigableSet
Collections.unmodifiableMap Collections.unmodifiableSortedMap
Collections.unmodifiableNavigableMap
```
```