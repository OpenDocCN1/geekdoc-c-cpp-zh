+   • `static <E> List<E> asList(E... array)`

returns a list view of the elements in an array that is modifiable but not resizable.

# **java.util.List<E>** 1.2

+   • `List<E> subList(int firstIncluded, int firstExcluded)`

returns a list view of the elements within a range of positions.

# **java.util.SortedSet<E>** 1.2

+   • `SortedSet<E> subSet(E firstIncluded, E firstExcluded)`
+   • `SortedSet<E> headSet(E firstExcluded)`
+   • `SortedSet<E> tailSet(E firstIncluded)`

returns a view of the elements within a range.

# **java.util.NavigableSet<E>** 6

+   • `NavigableSet<E> subSet(E from, boolean fromIncluded, E to, boolean toIncluded)`
+   • `NavigableSet<E> headSet(E to, boolean toIncluded)`
+   • `NavigableSet<E> tailSet(E from, boolean fromIncluded)`

returns a view of the elements within a range. The boolean flags determine whether the bounds are included in the view.