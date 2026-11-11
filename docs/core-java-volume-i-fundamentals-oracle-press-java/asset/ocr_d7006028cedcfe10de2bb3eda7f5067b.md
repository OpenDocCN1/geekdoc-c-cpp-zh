```
```java
Arrays.sort(people, Comparator.comparing(Person::getName));
```
```

This is certainly much easier than implementing a comparator by hand.
Moreover, the code is clearer since it is obvious that we want to compare
people by name.

You can chain comparators with the `thenComparing` method for breaking ties.
For example,

```
```java
Arrays.sort(people,
    Comparator.comparing(Person::getLastName)
    .thenComparing(Person::getFirstName));
```
```

If two people have the same last name, then the second comparator is used.

There are a few variations of these methods. You can specify a comparator
to be used for the keys that the `comparing` and `thenComparing` methods
extract. For example, here we sort people by the length of their names:

```
```java
Arrays.sort(people, Comparator.comparing(Person::getName,
    (s, t) -> Integer.compare(s.length(), t.length())));
```
```

Moreover, both the `comparing` and `thenComparing` methods have variants that
avoid boxing of `int`, `long`, or `double` values. An easier way of producing the
preceding operation would be

```
```java
Arrays.sort(people, Comparator.comparingInt(p ->
    p.getName().length()));
```
```

If your key function can return `null`, you will like the `nullsFirst` and
`nullsLast` adapters. These static methods take an existing comparator and
modify it so that it doesn't throw an exception when encountering `null`
values but ranks them as smaller or larger than regular values. For example,
suppose `getMiddleName` returns a `null` when a person has no middle name.
Then you can use `Comparator.comparing(Person::getMiddleName,
Comparator.nullsFirst(. . .))`.