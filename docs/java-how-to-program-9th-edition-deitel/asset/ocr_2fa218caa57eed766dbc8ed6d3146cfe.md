to the end of links. Lines 17–18 call LinkedList method add to add "pink" as the last element and "green" as the element at index 3 (i.e., the fourth element). Method addLast (line 16) functions identically to method add (line 17). Line 19 calls LinkedList method addFirst to add "cyan" as the new first item in the LinkedList. The add operations are permitted because they operate on the LinkedList object, not the view returned by asList. [Note: When "cyan" is added as the first element, "green" becomes the fifth element in the LinkedList.]

Line 22 calls the List interface’s toArray method to get a String array from links. The array is a copy of the list’s elements—modifying the array’s contents does not modify the list. The array passed to method toArray is of the same type that you’d like method toArray to return. If the number of elements in that array is greater than or equal to the number of elements in the LinkedList, toArray copies the list’s elements into its array argument and returns that array. If the LinkedList has more elements than the number of elements in the array passed to toArray, toArray allocates a new array of the same type it receives as an argument, copies the list’s elements into the new array and returns the new array.

# Common Programming Error 20.2

Passing an array that contains data to toArray can cause logic errors. If the number of elements in the array is smaller than the number of elements in the list on which toArray is called, a new array is allocated to store the list’s elements—without preserving the array argument’s elements. If the number of elements in the array is greater than the number of elements in the list, the elements of the array (starting at index zero) are overwritten with the list’s elements. Array elements that are not overwritten retain their values.

# 20.7 Collections Methods

Class Collections provides several high-performance algorithms for manipulating collection elements. The algorithms (Fig. 20.5) are implemented as static methods. The methods sort, binarySearch, reverse, shuffle, fill and copy operate on Lists. Methods min, max, addAll, frequency and disjoint operate on Collections.

| Method | Description |
|---|---|
| sort | Sorts the elements of a List. |
| binarySearch | Locates an object in a List. |
| reverse | Reverses the elements of a List. |
| shuffle | Randomly orders a List’s elements. |
| fill | Sets every List element to refer to a specified object. |
| copy | Copies references from one List into another. |
| min | Returns the smallest element in a Collection. |
| max | Returns the largest element in a Collection. |
| addAll | Appends all elements in an array to a Collection. |
| frequency | Calculates how many collection elements are equal to the specified element. |
| disjoint | Determines whether two collections have no elements in common. |

Fig. 20.5 | Collections methods.