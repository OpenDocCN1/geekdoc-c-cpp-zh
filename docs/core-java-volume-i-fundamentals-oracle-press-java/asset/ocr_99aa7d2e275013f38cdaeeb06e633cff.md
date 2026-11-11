collections. We discuss these in [Section 9.5](#), “Copies and Views,” on p. 548.

Finally, Java 6 introduced interfaces `NavigableSet` and `NavigableMap` that contain additional methods for searching and traversal in sorted sets and maps. (Ideally, these methods should have simply been included in the `SortedSet` and `SortedMap` interface.) The `TreeSet` and `TreeMap` classes implement these interfaces.

# 9.3 Concrete Collections

[Table 9.1](#) shows the collections in the Java library and briefly describes the purpose of each collection class. (For simplicity, I omit the thread-safe collections that will be discussed in [Chapter 12](#).)

All classes in [Table 9.1](#) implement the `Collection` interface, with the exception of the classes with names ending in Map. Those classes implement the `Map` interface instead. We will discuss maps in [Section 9.4](#), “Maps,” on p. 535.

[Figure 9.5](#) shows the relationships between these classes.

**Table 9.1** Concrete Collections in the Java Library