
![](img/0e7b74ef51a065c077b42cd87b362288_728_0.png)

**Figure 9.5** Classes in the collections framework

### 9.3.1 Linked Lists

We already used arrays and their dynamic cousin, the `ArrayList` class, for many examples in this book. However, arrays and array lists suffer from a major drawback. Removing an element from the middle of an array is expensive since all array elements beyond the removed one must be moved toward the beginning of the array (see Figure 9.6). The same is true for inserting elements in the middle.

![](img/0e7b74ef51a065c077b42cd87b362288_729_0.png)

**Figure 9.6** Removing an element from an array

Another well-known data structure, the *linked list*, solves this problem. Where an array stores object references in consecutive memory locations, a linked list stores each object in a separate *link*. Each link also stores a reference to the next link in the sequence. In the Java programming language, all linked lists are actually *doubly linked*; that is, each link also stores a reference to its predecessor (see Figure 9.7).

![](img/0e7b74ef51a065c077b42cd87b362288_730_0.png)

**Figure 9.7** A doubly linked list

Removing an element from the middle of a linked list is an inexpensive operation—only the links around the element to be removed need to be updated (see *Figure 9.8*).

![](img/0e7b74ef51a065c077b42cd87b362288_731_0.png)

**Figure 9.8** Removing an element from a linked list

Perhaps you once took a data structures course in which you learned how to implement linked lists. You may have bad memories of tangling up the links when removing or adding elements in the linked list. If so, you will be pleased to learn that the Java collections library supplies a class `LinkedList` ready for you to use.

The following code example adds three elements and then removes the second one:

```java
var staff = new LinkedList<String>();
staff.add("Amy");
staff.add("Bob");
staff.add("Carl");
Iterator<String> iter = staff.iterator();
String first = iter.next(); // visit first element
String second = iter.next(); // visit second element
iter.remove(); // remove last visited element
```

There is, however, an important difference between linked lists and generic collections. A linked list is an *ordered collection* in which the position of the objects matters. The `LinkedList.add` method adds the object to the end of the list. But you will often want to add objects somewhere in the middle of a list. This position-dependent add method is the responsibility of an iterator, since iterators describe positions in collections. Using iterators to add elements makes sense only for collections that have a natural ordering. For example, the *set* data type that we discuss in the next section does not impose any ordering on its elements. Therefore, there is no add method in the `Iterator` interface. Instead, the collections library supplies a subinterface `ListIterator` that contains an add method:

```java
interface ListIterator<E> extends Iterator<E>
{
    void add(E element);
    . . .
}
```

Unlike `Collection.add`, this method does not return a `boolean`—it is assumed that the add operation always modifies the list.

In addition, the `ListIterator` interface has two methods that you can use for traversing a list backwards.

```java
E previous();
boolean hasPrevious();
```

Like the next method, the previous method returns the object that it skipped over.

The `listIterator` method of the `LinkedList` class returns an iterator object that implements the `ListIterator` interface.

```java
ListIterator<String> iter = staff.listIterator();
```

The add method adds the new element *before* the iterator position. For example, the following code skips past the first element in the linked list and adds "Juliet" before the second element (see *Figure 9.9*):

```java
var staff = new LinkedList<String>();
staff.add("Amy");
staff.add("Bob");
staff.add("Carl");
ListIterator<String> iter = staff.listIterator();
iter.next(); // skip past first element
iter.add("Juliet");
```

![](img/0e7b74ef51a065c077b42cd87b362288_734_0.png)

**Figure 9.9** Adding an element to a linked list

If you call the add method multiple times, the elements are simply added in the order in which you supplied them. They are all added in turn before the current iterator position.

When you use the add operation with an iterator that was freshly returned from the listIterator method and that points to the beginning of the linked list, the newly added element becomes the new head of the list. When the iterator has passed the last element of the list (that is, when hasNext returns *false*), the added element becomes the new tail of the list. If the linked list has *n* elements, there are *n + 1* spots for adding a new element. These spots correspond to the *n + 1* possible positions of the iterator. For example, if a linked list contains three elements, A, B, and C, there are four possible positions (marked as |) for inserting a new element:

| 位置 |
| --- |
| \|ABC |
| A\|BC |
| AB\|C |
| ABC\| |

**NOTE:**

Be careful with the “cursor” analogy. The remove operation does not work exactly like the Backspace key. Immediately after a call to next, the remove method indeed removes the element to the left of the iterator, just like the Backspace key would. However, if you have just called previous, the element to the right will be removed. And you can’t call remove twice in a row.

Unlike the add method, which depends only on the iterator position, the remove method depends on the iterator state.

Finally, a set method replaces the last element, returned by a call to next or previous, with a new element. For example, the following code replaces the first element of a list with a new value:

```java
ListIterator<String> iter = list.listIterator();
String oldValue = iter.next(); // returns first element
iter.set(newValue); // sets first element to newValue
```

As you might imagine, if an iterator traverses a collection while another iterator is modifying it, confusing situations can occur. For example, suppose an iterator points before an element that another iterator has just removed. The iterator is now invalid and should no longer be used. The linked list iterators have been designed to detect such modifications. If an iterator finds that its collection has been modified by another iterator or by a method of the collection itself, it throws a `ConcurrentModificationException`. For example, consider the following code:

```java
List<String> list = . . .;
ListIterator<String> iter1 = list.listIterator();
ListIterator<String> iter2 = list.listIterator();
iter1.next();
iter1.remove();
iter2.next(); // throws ConcurrentModificationException
```

The call to `iter2.next` throws a `ConcurrentModificationException` since `iter2` detects that the list was modified externally.

To avoid concurrent modification exceptions, follow this simple rule: You can attach as many iterators to a collection as you like, provided that all of them are only readers. Alternatively, you can attach a single iterator that can both read and write.

Concurrent modification detection is done in a simple way. The collection keeps track of the number of mutating operations (such as adding and removing elements). Each iterator keeps a separate count of the number of mutating operations that it was responsible for. At the beginning of each iterator method, the iterator simply checks whether its own mutation count equals that of the collection. If not, it throws a `ConcurrentModificationException`.

![](img/0e7b74ef51a065c077b42cd87b362288_736_0.png)

> **NOTE:**
>
> There is, however, a curious exception to the detection of concurrent modifications. The linked list only keeps track of *structural* modifications to the list, such as adding and removing links. The `set` method does *not* count as a structural modification. You can attach multiple iterators to a linked list, all of which call `set` to change the contents of existing links. This capability is required for a number of algorithms in the `Collections` class that we discuss later in this chapter.

Now you have seen the fundamental methods of the `LinkedList` class. Use a `ListIterator` to traverse the elements of the linked list in either direction and to add and remove elements.

As you saw in Section 9.2, “Interfaces in the Collections Framework,” on p. 508, many other useful methods for operating on linked lists are declared in the `Collection` interface. These are, for the most part, implemented in the `AbstractCollection` superclass of the `LinkedList` class. For example, the `toString` method invokes `toString` on all elements and produces one long
