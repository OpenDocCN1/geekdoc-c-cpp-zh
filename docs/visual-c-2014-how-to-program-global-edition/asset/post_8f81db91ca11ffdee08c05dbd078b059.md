
928 Chapter 21 Generic Collections: Functional Programming with LINQ/PLINQ

- hash function
- hash table
- hashing
- IComparer<T> interface
- IEnumerable<T> interface
- IEnumerator<T> interface
- immutability
- index indexizer
- indexer of class SortedDictionary<K,V>
- IndexOf method class Array
- internal relation
- Keys of class SortedDictionary<K,V>
- KeyValuePair<K,V> type
- lambda
- lambda expression
- Last property of class LinkedList<T>
- LastIndexOf method class Array
- LinkedList<T> class
- LinkedListNode<T> class
- load factor in a hash map
- map operation in functional programming
- MaxEnumerable<T> extension method
- MaxParallelQuery<T> extension method
- MinEnumerable<T> extension method
- MinParallelQuery<T> extension method
- MoveNext method of interface IEnumerator<T>
- Next property of class LinkedListNode<T>
- Now property of type DateTime
- OrderByIEnumerable<T> extension method
- ParallelEnumerable<T> class
- ParallelQuery<T> interface

PLINQ (Parallel LINQ)
- Previous property of class LinkedListNode<T>
- Queue<T> collection
- Range method of class Enum
- reduction operation in functional programming
- Remove method of class LinkedList<T>
- Reset method of interface IEnumerator<T>
- Reverse method of class Array
- Select<T> extension method
- Sort method of class Array
- SortedDictionary<K,V> collection
- SortedList<K,V> collection
- SortedSet<T> collection
- Stack<T> class
- statement lambda
- Subtract method of type DateTime
- Sum<T> extension method
- System.Collections namespace
- System.Collections.Concurrent namespace
- System.Collections.Generic namespace
- System.Collections.Specialized namespace
- TimeSpan
- ToArray method of class Enumerable
- ToList method of class Enumerable
- TotalMilliseconds property of type TimeSpan
- using static directive
- Value property of class LinkedListNode<T>
- Values property of class SortedDictionary<K,V>
- Where IEnumerable<T> extension method

# Self-Review Exercises

+ 21.1 Fill in the blanks in each of the following statements:
a) A(n) is used to iterate through a collection but cannot remove elements from the collection during the iteration.
b) IEnumerator method advances the enumerator to the next item.
c) If the collection has been altered since the enumerator’s creation, calling method Reset will cause a(n).
d) C# s directive allows access to a class's static members without fully qualifying their names.
e) The statement implicitly obtains an enumerator via the GetEnumerator method and uses the MoveNext method and Current property to traverse the collection.
f) A(n) is a collection of key-value pairs.
g) allow you to define simple, anonymous methods—that is, methods that do not have names and are defined that are assigned to a delegate or passed a delegate parameter.
h) With you specify how to iterate, not the library.
i) With the library determines how to iterate through a collection.

# Answers to Self-Review Exercises

+ j) Functional programming, a(n) ________ operation results in a new collection containing only the elements that satisfy a condition.

+ k) Functional programming, a(n) operation results in a new collection in which each element of the original collection is mapped to a new value (possibly of a different type). The new collection has the same number of elements as the collection that was mapped.

+ l) Functional programming, a(n) operation combines the elements of a collection into a new value, typically using a lambda to specify how to combine the elements.

+ m) To parallel processing with LINQ, use IEnumerable<T> extension method (from ParallelEnumerable) which returns an a(n)

# 21.2 State whether each of the following is true or false. If false, explain why.

+ a) Functional programming's filter, map and reduce operations correspond to the IEnumerable<T> extension methods, Select and Aggregate.

+ b) Hashtables key-value pairs.

+ c) A class implementing enumerator<T> must define only methods MoveNext and Reset.

+ d) Dictionary<k,v> can contain duplicate keys.

+ e) LinkedList<T> can contain duplicate values.

+ f) Dictionary is an interface.

+ g) Enumerators change the values of elements but cannot remove them.

+ h) With hashing, the load factor increases, the chance of collisions increases.

+ i) Elements in an array must be sorted in order before a BinarySearch may be performed.

+ j) Array provides static method Sort for sorting elements.

+ k) A hash table is one way to implement a dictionary.

+ l) The ? determines whether an array or collection is null before accessing an element of the array.

+ m) Lambda expression begins with a parameter list and is followed by the => lambda operator and represents the lambda's body.

+ n) An expression contains a statement block—one or more statements enclosed in braces {}—to the right of the lambda operator.

+ o) The parentheses surrounding a lambda's parameter list are optional.

+ p) A key aspect of functional programming is immutability—not modifying the data source because or other program state, such as counter-control variables in loops. This eliminates common errors that caused by modifying data incorrectly.

# Answers to Self-Review Exercises

+ 21.1 a enumerator (or foreach statement). b MoveNext. c InvalidOperationException. d static constructor. f dictionary. g Lambda expressions. h external iteration. i internal iteration. j filter. k map. l reduce. AsParallel, ParallelQuery<T>.

+ 21.2 a True. b False. c False. d False. e True. f False. g False. h True. i True. j True. k True. l True. m True. n False. o False. p True.

# Exercises

## 21.3 (Collections Terminology)
Describe each of the following:
- a) ICollection
- b) Array
- c) IList
- d) load factor
- e) hash-table
- f) space-time trade-off
- g) dictionary

## 21.4 (Enumerator Members)
Explain briefly each of the following enumerator-related methods:
- a) GetEnumerator
- b) Current
- c) MoveNext

## 21.5 (IDictionary<K,V> Methods and Properties)
Explain briefly the following methods of IDictionary<K,V>, which both Dictionary and SortedDictionary implement:
- a) Add
- b) Keys
- c) Values
- d) ContainsKey

## 21.6 (LinkedList without Duplicates)
Write an app that reads a series of names and stores them in a LinkedList. Do not store duplicate names. Allow the user to search for a name.

## 21.7 (Summarizing Counts with SortedDictionary)
Modify the app in 2.4 to count the number of occurrences of each name rather than each word. For example, the "HELLO THERE" contains two Hs, three Es, two Ls, one O, one T and one R. Display the results.

(Dictionary of Colors)
Use SortedDictionary to create a reusable class for choosing from the predefined colors in Color (in the System.Drawing namespace). The names of the colors should be used as keys, and the Color objects should be used as values. Place this class in a class library that can be referenced from any C#. Use your new class in a Windows app that allows the user to select a color, then change the background color of the Form.

(Duplicate Words in a Sentence)
Write an app that determines and displays the number of duplicate words in a sentence. Treat uppercase and lowercase the letters as same. Ignore punctuation.

(Using a List)
Write an app that inserts 25 random integers from 0 to 100 into an order of class List. The app should calculate the sum of the elements and the floating-point average of the elements. Use loops to help perform calculations.

(Reversing a LinkedList)
Write an app that creates a LinkedList object of 10 characters, creates a second list containing a copy of the file, but in reverse order. Do not call method method.

(Prime Numbers and Prime Factorization)
Write an app that takes a whole-number from a user and determines whether it's prime. If the number is not prime, display the unique prime factors of the number (using a List<int> to store the factors). Remember that a prime number's factors are only 1 and the prime itself. Every number that's not prime has a unique prime factorization. For example, consider the number 54. The prime factors of 54 are 2, 3, 3 and 3. When
