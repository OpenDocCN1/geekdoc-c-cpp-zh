# TABLE 1-3 The collection of functions

| Function | Array | List | Seq | Map | Set | Description |
| --- | --- | --- | --- | --- | --- | --- |
| append | O(m+n) | O(min,n) | O(1) | | | Concatenates two collections. |
| add | | | | O(logN) | O(logN) | Adds a new element, and returns a new collection. |
| average /averageBy | O(n) | O(n) | O(n) | | | Gets an average of all elements. |
| blit | O(n) | | | | | Returns a slice of the array. |
| cache | | | O(n) | | | Caches elements. |
| cast | | | O(n) | | | Converts an element to a specified type. |
| choose | O(n) | O(n) | O(n) | | | Chooses the element if not return None. |
| collect | O(n) | O(n) | O(n) | | | Applies a function to each element, and concatenates the results. |
| compareWith | | | O(n) | | | Compares element by element using a given function. |
| concat | O(n) | O(n) | O(n) | | | Concatenates two collections. |
| contains | | | | | O(logN) | Tests whether contains the specified element. |
| containsKey | | | | O(logN) | | Tests whether an element is in the domain of the map. |
| count | | | | | O(logN) | Counts the number of elements in the set. |
| countBy | | | O(n) | | | Counts the generated key numbers. The key is generated from a function. |
| copy | O(n) | | O(n) | | | Creates a copy of the collection. |
| create | O(n) | | | | | Creates an array. |
| delay | | | O(1) | | | Returns a sequence that is built from the given specification of a sequence. |
| difference | | | | | O(m*logN) | Returns a new set with an element in set1 but not set2. |
| distinct/ /distinctBy | | | O(1) | | | Returns a new seq with removing duplicated elements. |
| empty | O(1) | O(1) | | O(1) | O(1) | Creates an empty collection. |
| exists | O(n) | O(n) | O(n) | O(logN) | O(logN) | Tests if any element satisfies the condition. |
| exists2 | O(min(n,m)) | | O(min(n,m)) | | | Tests whether any pair of corresponding elements of the input sequences satisfies the given predicate. |
| fill | O(n) | | | | | Sets the range of element to a specified value.