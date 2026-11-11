
string of the format `[A, B, C]`. This is handy for debugging. Use the `contains` method to check whether an element is present in a linked list. For example, the call `staff.contains("Harry")` returns true if the linked list already contains a string equal to the string "Harry".

The library also supplies a number of methods that are, from a theoretical perspective, somewhat dubious. Linked lists do not support fast random access. If you want to see the *n*th element of a linked list, you have to start at the beginning and skip past the first *n − 1* elements. There is no shortcut. For that reason, programmers don’t usually use linked lists in situations where elements need to be accessed by an integer index.

Nevertheless, the `LinkedList` class supplies a `get` method that lets you access a particular element:

```java
LinkedList<String> list = . . .;
String obj = list.get(n);
```

Of course, this method is not very efficient. If you find yourself using it, you are probably using a wrong data structure for your problem.

You should *never* use this illusory random access method to step through a linked list. The code

```java
for (int i = 0; i < list.size(); i++)
    do something with list.get(i);
```

is staggeringly inefficient. Each time you look up another element, the search starts again from the beginning of the list. The `LinkedList` object makes no effort to cache the position information.

![](img/0e7b74ef51a065c077b42cd87b362288_737_0.png)

> **NOTE:**
> 
> The `get` method has one slight optimization: If the index is at least `size() / 2`, the search for the element starts at the end of the list.

The list iterator interface also has a method to tell you the index of the current position. In fact, since Java iterators conceptually point between elements, it has two of them: The `nextIndex` method returns the integer index of the element that would be returned by the next call to `next`; the `previousIndex` method returns the index of the element that would be returned by the next call to `previous`. Of course, that is simply one less than `nextIndex`. These methods are efficient—an iterator keeps a count of its current position. Finally, if you have an integer index `n`, then `list.listIterator(n)` returns an iterator that points just before the element with index `n`. That is, calling `next` yields the same element as `list.get(n)`; obtaining that iterator is inefficient.

If you have a linked list with only a handful of elements, you don't have to be overly paranoid about the cost of the `get` and `set` methods. But then, why use a linked list in the first place? The only reason to use a linked list is to minimize the cost of insertion and removal in the middle of the list. If you have only a few elements, you can just use an `ArrayList`.

I recommend that you simply stay away from all methods that use an integer index to denote a position in a linked list. If you want random access into a collection, use an array or `ArrayList`, not a linked list.

The program in Listing 9.1 puts linked lists to work. It simply creates two lists, merges them, then removes every second element from the second list, and finally tests the `removeAll` method. I recommend that you trace the program flow and pay special attention to the iterators. You may find it helpful to draw diagrams of the iterator positions, like this:

```text
|ACE    |BDFG
A|CE    |BDFG
AB|CE  B|DFG
. . .
```

Note that the call

```java
System.out.println(a);
```

prints all elements in the linked list a by invoking the `toString` method in `AbstractCollection`.

### Listing 9.1 `linkedList/LinkedListTest.java`

```java
package linkedList;

import java.util.*;

/**
 * This program demonstrates operations on linked lists.
 * @version 1.12 2018-04-10
 * @author Cay Horstmann
 */
public class LinkedListTest
{
   public static void main(String[] args)
   {
      var a = new LinkedList<String>();
      a.add("Amy");
      a.add("Carl");
      a.add("Erica");

      var b = new LinkedList<String>();
      b.add("Bob");
      b.add("Doug");
      b.add("Frances");
      b.add("Gloria");

      // merge the words from b into a

      ListIterator<String> aIter = a.listIterator();
      Iterator<String> bIter = b.iterator();

      while (bIter.hasNext())
      {
         if (aIter.hasNext()) aIter.next();
         aIter.add(bIter.next());
      }

      System.out.println(a);

      // remove every second word from b

      bIter = b.iterator();
      while (bIter.hasNext())
      {
         bIter.next(); // skip one element
         if (bIter.hasNext())
         {
            bIter.next(); // skip next element
            bIter.remove(); // remove that element
         }
      }

      System.out.println(b);

      // bulk operation: remove all words in b from a

      a.removeAll(b);

      System.out.println(a);
   }
}
```

### `java.util.List<E>` 1.2

- `ListIterator<E> listIterator()`  
  returns a list iterator for visiting the elements of the list.
- `ListIterator<E> listIterator(int index)`  
  returns a list iterator for visiting the elements of the list whose first call to `next` will return the element with the given index.
- `void add(int i, E element)`  
  adds an element at the specified position.
- `void addAll(int i, Collection<? extends E> elements)`  
  adds all elements from a collection to the specified position.
- `E remove(int i)`  
  removes and returns the element at the specified position.
- `E get(int i)`  
  gets the element at the specified position.
- `E set(int i, E element)`  
  replaces the element at the specified position with a new element and returns the old element.
- `int indexOf(Object element)`  
  returns the position of the first occurrence of an element equal to the specified element, or −1 if no matching element is found.
- `int lastIndexOf(Object element)`  
  returns the position of the last occurrence of an element equal to the specified element, or −1 if no matching element is found.

### `java.util.ListIterator<E>` 1.2

- `void add(E newElement)`  
  adds an element before the current position.
- `void set(E newElement)`  
  replaces the last element visited by `next` or `previous` with a new element. Throws an `IllegalStateException` if the list structure was modified since the last call to `next` or `previous`.
- `boolean hasPrevious()`  
  returns true if there is another element to visit when iterating backwards through the list.
- `E previous()`  
  returns the previous object. Throws a `NoSuchElementException` if the beginning of the list has been reached.
- `int nextIndex()`  
  returns the index of the element that would be returned by the next call to `next`.
- `int previousIndex()`  
  returns the index of the element that would be returned by the next call to `previous`.

### `java.util.LinkedList<E>` 1.2

- `LinkedList()`  
  constructs an empty linked list.
- `LinkedList(Collection<? extends E> elements)`  
  constructs a linked list and adds all elements from a collection.
- `void addFirst(E element)`
- `void addLast(E element)`  
  adds an element to the beginning or the end of the list.
- `E getFirst()`
- `E getLast()`  
  returns the element at the beginning or the end of the list.
- `E removeFirst()`
- `E removeLast()`  
  removes and returns the element at the beginning or the end of the list.

## 9.3.2 Array Lists

In the preceding section, you saw the `List` interface and the `LinkedList` class that implements it. The `List` interface describes an ordered collection in which the position of elements matters. There are two protocols for visiting the elements: through an iterator and by random access with methods `get` and `set`. The latter is not appropriate for linked lists, but of course `get` and `set` make a lot of sense for arrays. The collections library supplies the familiar `ArrayList` class that also implements the `List` interface. An `ArrayList` encapsulates a dynamically reallocated array of objects.

![](img/0e7b74ef51a065c077b42cd87b362288_743_0.png)

> **NOTE:**
> 
> If you are a veteran Java programmer, you may have used the `Vector` class whenever you need a dynamic array. Why use an `ArrayList` instead of a `Vector`? For one simple reason: All methods of the `Vector` class are *synchronized*. It is safe to access a vector object from two threads. But if you access a vector from only a single thread—by far the more common case—your code wastes quite a bit of time with synchronization. In contrast, the `ArrayList` methods are not synchronized. I recommend that you use an `ArrayList` instead of a `Vector` whenever you don’t need synchronization.

## 9.3.3 Hash Sets

Linked lists and arrays let you specify the order in which you want to arrange the elements. However, if you are looking for a particular element and don’t remember its position, you need to visit all elements until you find a match. That can be time consuming if the collection contains many elements. If you don’t care about the ordering of the elements, there are data structures that let you find elements much faster. The drawback is that those data structures give you no control over the order in which the elements appear. These data structures organize the elements in an order that is convenient for their own purposes.

A well-known data structure for finding objects quickly is the *hash table*. A hash table computes an integer, called the *hash code*, for each object. A hash code is somehow derived from the instance fields of an object, preferably in
