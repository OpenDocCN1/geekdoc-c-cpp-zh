element X is considered to be equal to element Y, and element Y is considered to be equal to element Z, all three elements X, Y, and Z must be considered equal to one another. If an element X is considered to be greater than Y, Y must be considered to be less than X. And there must be no “transitivity paradoxes”—that is, you cannot have X greater than Y, Y greater than Z, and Z greater than X. If you fail to provide a total ordering, the action of the sort algorithm is undefined; it may produce a crazy ordering, it may crash, it may go into an infinite loop, and so on.

Notice, for example, how the comparer in Listing 17.2 ensures a total order, even if the arguments are null references. It would not be legal to say, “If either element is null, then return zero,” for example, because then two non-null things could be equal to null but not equal to each other.

> **Guidelines**

DO ensure that custom comparison logic produces a consistent “total order.”

# Searching a List<T>

To search List<T> for a particular element, you use the Contains(), IndexOf(), LastIndexOf(), and BinarySearch() methods. The first three methods search through the array, starting at the first element (or the last element for LastIndexOf()), and examine each element until the desired one is found. The execution time for these algorithms is proportional to the number of elements searched before a hit occurs. (Be aware that the collection classes do not require that all the elements within the collection are unique. If two or more elements in the collection are the same, IndexOf() returns the first index and LastIndexOf() returns the last index.)

BinarySearch() uses a much faster binary search algorithm but requires that the elements be sorted. A useful feature of the BinarySearch() method is that if the element is not found, a negative integer is returned. The bitwise complement (¬) of this value is the index of the next element larger than the element being sought, or the total element count if there is no greater value. This provides a convenient means to insert new values into the list at the specific location so as to maintain sorting. Listing 17.3 provides an example.