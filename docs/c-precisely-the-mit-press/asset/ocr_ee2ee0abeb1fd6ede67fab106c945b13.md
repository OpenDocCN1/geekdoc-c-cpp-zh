188 Generic Collections: Sets, Lists, and Dictionaries

# 27.6 The List<T> Class

The generic class List<T> implements IList<T> and IList. The elements are stored in an array that grows as needed elements are added. Element access is fast, but insertion and deletion are costly except at the list's end. Class List<T> has the members defined by IList<T> and these, among others:

+   - Constructor List<T>() creates an empty list.
- Constructor List<T>(int capacity) creates an empty list with a given initial capacity.
- Constructor List<T>(IEnumerable<T> enm) creates a list containing enm.elements.
- Read-write property int Capacity gets or sets the current capacity of the list. Throws ArgumentOutOf if capacity is less than the number of elements.
- void AddRange(IEnumerable<T> enm) adds elements to the end of the list.
- IList<T> AsReadOnly() returns a read-only list that is a wrapper around the given list.
- int BinarySearch(T x) searches for x using binary search. Returns index i>=0 for a[i].CompareTo(x) == 0; otherwise returns i such that -i would be the position for k. The list must be sorted, or call Sort(cmp); else the result is undefined.
- int BinarySearch(T x, IComparer<T> cmp) works similarly, but compares elements using cmp.Compare. The list must be sorted, or call Sort(cmp); else the result is undefined.
- int BinarySearch(int i, int n, IComparer<T> cmp) works similarly, but searches the list with indices i..(n-1).
- void CopyTo(int src, T[] arr, int dat, int n) copies n elements starting at position src to the array arr, starting at position dat. Throws ArgumentOutOfRangeException if src<0 or dat<0 or n<0.
- int IndexOf(T x, int i) returns the least index greater than or equal to i which element equals x; otherwise returns -1. Throws ArgumentOutOfRangeException if i<0 or i>Count.
- int IndexOf(T x) returns the least index greater than 0 and smaller than Count element x; and two other overloads are similar to IndexOf but return the greater index than the least index at an element equals x.
- void RemoveRange(int i, int n) removes the elements in range i..(n-1).
- void Reverse() reverses the order of the list.
- void Reverse(int i, int n) reverses the elements in range i..(n-1).
- void Sort() sorts the list using quicksort, comparing elements using their CompareTo method. The list elements must implement IComparable<T>. The sort is not stable.
- void Sort(IComparer<T> cmp) sorts the list, comparing elements using cmp.Compare.
- void Sort(int i, int n, IComparer<T> cmp) sorts the segment with indices i..(n-1).
- T[] ToArray() returns a new array containing the elements of the list.
- void TrimSize() shrinks the list's capacity to the actual number of elements.