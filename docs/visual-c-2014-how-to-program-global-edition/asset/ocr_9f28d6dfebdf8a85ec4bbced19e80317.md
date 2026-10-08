# Terminology 927

+   - DateTime method Subtract compute the difference between two DateTimes, which is returned as a TimeSpan.

+   - TimeSpan.TotalMilliseconds returns the number of milliseconds represented by the TimeSpan.

+   - To initiate parallel processing, invoke IParallel<T> extension method AsParallel(from class ParallelEnumerable), which returns a ParallelQuery<T>.

+   - An object that implements ParallelQuery<T> can be used with PLINQ to parallelize versions of the LINQ extension methods.

+   - ClassEnumerable defines the ParallelQuery<T> (PLINQ) parallelized versions of LINQ to Objects extension methods as well as several PLINQ-specific extension methods.

# Section 21.13 (Optional) Covariance and Contravariance for Generic Types

+   - C supports covariance and contravariance of generic interface and delegate types.

+   - Assigning an array of a derived-class to an array variable of a base-class type is an example of covariance.

+   - Covariance works with several generic interfaces, including IEnumerable<T>.

+   - Using a cast to assign an array variable of a base-class type to an array variable of a derived-class type is an example of contravariance.

+   - SortedSet maintains a set of objects in sorted order--no duplicates are allowed.

+   - The objects in a SortedSet must be comparable to determine their sorting order. Objects are compared if their classes implement IComparable<T> interface.

+   - For classes that do not implement IComparable<T>, you can compare the objects using an object that implements IComparable<T> interface. This compare method compares its two arguments and returns 0 if they are equal, a negative integer if the first is less than the second, or a positive integer if the first object is greater than the second.

+   - Providing an IComparer for a base-class type where an IComparer for a derived-class type is expected because IComparer<T> supports covariance.

# Terminology

```
?[] null-conditional operator
=> lambda operator
Add method of class SortedDictionary<K,V>
AddFirst method of class LinkedList<T>
AddLast method of class LinkedList<T>
Aggregate IEnumerable<T> extension method
anonymous method
AsParallel method
Average IEnumerable<T> extension method
AverageParallelQuery<T> extension method
BinarySearch method of class Array
Clear method of class Array
collection class
collision in a hash table
ContainsKey method of class
SortedDictionary<K,V>
contravariance
```

```
Copy method of class Array
Count property of class SortedDictionary<K,V>
covariance
CreateInstance method of class Array
Current property of interface IEnumerable<T>
dictionary<K,V> collection
enumerable class
enumerator
expression lambda
Find method of class LinkedList<T>
nternal iteration
filter operation in functional programming
Func delegate
functional programming
GetEnumerator method of interface IEnumerable<T>
HashCode method of class object
```