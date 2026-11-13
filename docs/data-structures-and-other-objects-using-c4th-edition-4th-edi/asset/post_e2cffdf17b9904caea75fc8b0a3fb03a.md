
- 15. The bag implementation uses the copy function from the <algorithm> facility. Why do we need to write the full name std::copy in the implementation of the bag template, but we write the shorter version, copy, in the implementation of the ordinary class?

- 16. Write declarations for three bags with three different item types. Can you use all three bags in a single program?

## 6.3 THE STL'S ALGORITHMS AND USE OF ITERATORS

### STL Algorithms

Now that you know how to write your own template classes, we can examine more details of the Standard Template Library. The STL contains a group of functions in the <algorithm> facility that can manipulate containers including the multiset (see page 139), the set (which is like the multiset but with no repeated items), and the map and multimap classes (both discussed in Chapter 12). We have already seen one example of an STL function: the copy function on page 116. Another example is the set_union function:

```
iterator set_union (iterator1 first1, iterator1 last1,
iterator2 first2, iterator2 last2,
iterator3 result);
```

This function can be used to create a union of two sets. In other words, it can create a new set that includes copies of all the elements from two other containers. The five parameters, which are all iterators (see page 140), need some explanation.

The first two parameters, first1 and last1, are iterators in a set. All the elements in the range [first1...last1) will be copied to the result. Notice that this range is a left-inclusive pattern using one square bracket and one parenthesis, so that the current element of the first iterator is included, but the range ends just before the last iterator. The first2 and last2 parameters define a second left-inclusive range [first2...last2), which is also copied to the result.

The location for the result is determined by the fifth parameter. This parameter, called result, must be an **output iterator**, which is a kind of iterator that provides an alternative way to insert new elements into a container. Programmers don't usually use output iterators directly, but they often use them as an argument to one of the STL algorithms. One way to create an output iterator for a container class called c is with the expression `inserter(c, c.begin())`.

The following code creates two sets, uses the set_union function to create a union of the sets, and iterates through the result.

some of the STL algorithms use output iterators to add new items to a container

```
set<string> actors1;
set<string> actors2;
set<string> result;
set<string>::iterator role;

actors1.insert("moe");
actors1.insert("curly");
actors2.insert("larry");
actors2.insert("curly");
```

```
// Notice how we create the output operator for the fifth argument:
set_union(actors1.begin(), actors1.end(),
actors2.begin(), actors2.end(),
inserter(result,result.begin()));
```

```
for (role = result.begin(); role != result.end(); ++role)
{
cout << *role << " ";
}
cout << endl;
```

The output shows all three actors in the union, with only one copy of the duplicate curly:

curly larry moe

By the way, each iterator in the STL actually has an ordinary version and a const version. The const version can be used when a program needs to access the elements of a container without changing them. For example, the role iterator shown above could have been a set<string>::const_iterator.

### Standard Categories of Iterators

The C++ Standard specifies five significant categories of iterators, based on their abilities. In order to use some of the built-in algorithms provided by the C++ Standard, a programmer must know which category is provided by a container class. The first two categories—an input iterator and an output iterator—are specialized iterators for retrieving and inserting elements. The other three categories are the forward iterator, the bidirectional iterator, and the random access iterator. Each of these categories has increasingly stronger abilities.

We'll finish this section with a list of each category's abilities.

### Output iterator.

We've already seen one example of an output iterator, as the final parameter for the set_union function on page 313. The current element of an output iterator can be assigned to, such as *p = "shemp"; for an output iterator called p. The ++ increment operator moves the iterator forward to another item. The intention is that an algorithm that uses an output iterator will do an assignment followed by an increment (++), over and over again. However, the output iterator itself cannot be used to retrieve those elements, so the output iterator's usefulness is limited to the situation where some algorithm needs to put a sequence of elements in a container or other object with an output iterator.

### Input iterator.

An input iterator is designed to provide a sequence of values. The current element of an input iterator can be retrieved by using the dereferencing * operator such as x = *p; for an input iterator called p. The ++ increment operator moves the iterator forward to another item. The intention is that an algorithm that uses an input iterator will retrieve an element (with the dereferencing *) followed by an increment (++), over and over again. The end of an input iterator's elements is usually detected by comparing the input iterator with another iterator that is known to be just beyond the end of the input range.

### Forward iterator.

A forward iterator p is an object that provides these items:

- Iterators have a default constructor (to create an iterator that is not yet initialized), a copy constructor, and an assignment operator.
- The * operator accesses the iterator's current item. In some cases, the item is assignable (meaning it can be directly changed in an assignment such as *p = "shemp"); in other cases, direct changes of the item are forbidden.
- The ++ operator moves the iterator forward to the next item. The operator can be used in prefix notation (such as ++p) or postfix notation (such as p++). Both versions move the iterator forward, and both versions are actually function calls that return an iterator (which can be used as part of a larger expression). In particular, ++p returns the iterator after it has moved forward, whereas p++ returns a copy of the iterator before it moved.
- Iterators can be tested for equality (p == q) and inequality (p != q). Two iterators over the same container are equal if their current items are in the same position, or if they are both past the end of the container. Iterators from different containers should not be compared with each other.

### Bidirectional iterator.

A bidirectional iterator has all the abilities of a forward iterator, plus it can move backward with the -- operator. The -- operator moves the iterator p backward one position (and returns the iterator after it has moved backward). The p-- operator also moves the iterator backward one position (and returns a copy of the iterator before it moved). As an example, the multiset::const_iterator is a bidirectional iterator.

### Random access iterator.

The term random access refers to the ability to quickly access any randomly selected location in a container. A random access iterator allows this quick access by providing six new operations in addition to those of the bidirectional iterator. Appendix H covers these six operations in detail. For now, you should know that a random access iterator p can use the notation p[n] to provide access to the item that is steps in front of the current item. For example, p[0] is the current item, p[1] is the next item, and so on. In addition, a random access iterator can always be used as if it were any of the other types of iterators because it has all of the same operations.

### Iterators for Arrays

A random access iterator looks a lot like an array. In fact, the opposite is also true: C++ will allow any pointer to an element in an array to be used as if it were a random access iterator. The "current item" of such a pointer is the array element that it points to. The ++ and -- operators move the pointer forward or backward one spot. And for a pointer p, the notation p[i] refers to the item that is i steps ahead of the current item.

Since a pointer to an array is a random access iterator, we can use these pointers in Standard Library functions that expect an iterator. For example, the copy function from <algorithm> is a template function with this prototype:

```
template <class SourceIterator, class DestinationIterator>
DestinationIterator copy(
    SourceIterator source_begin,
    SourceIterator source_end,
    DestinationIterator destination_begin
);
```

the [...] pattern occurs again

Both source_begin and source_end are iterators over the same object. The function copies elements from the source to the destination. The first element that is copied comes from source_begin, and the copying continues up to (but not including) source_end. Notice that this is another value of the left-inclusive pattern [...] that we have seen before. The return value is an iterator that is one position beyond the last copied element in the destination.

Anyway, we wanted to show you how an array can be used as an iterator in the arguments of the copy function. Here are some typical examples:

```
int numbers[7] = { 0, 10, 20, 30, 40, 50, 60 };
int small[3];
int *p = numbers + 2;       // An iterator that starts at numbers[2]
int *mid = numbers + 5;     // An iterator that starts at numbers[5]
int *small_front = small;   // An iterator that starts at small[0]

// p, mid, and small can all be used as iterators in the copy function.
// This will copy numbers[2]...numbers[4] into small:
copy(p, mid, small_front);

// The name of an array itself can also be used as the argument for an
// iterator (either by itself or with an offset such as numbers + 6).
// This statement copies the last three elements of numbers into small.
// Notice that numbers + 7 is one step beyond the end of the numbers
// array.
copy(numbers + 4, numbers + 7, small);
```
