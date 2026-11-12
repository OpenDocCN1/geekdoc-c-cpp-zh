
Two behaviors involve removing entries from a bag: remove a particular entry and remove all entries. Suppose we name the methods and any parameters and begin to specify them in pseudocode as follows:

```
// Removes one occurrence of a particular entry from the bag, if possible.
remove(anEntry)
```

```
// Removes all entries from the bag.
clear()
```

What return types are these methods?
The remove method won't be able to remove a given entry if it isn't in the bag. We will have the method return a boolean value, much as add does, so it can indicate success or not. Thus, the UML specification for the method is

```
+remove(anEntry: ItemType): boolean
```

The method clear can be a void method: We just want to empty the bag, not get any of its contents. Thus, we refine its specification as follows:

```
+clear(): void
```

The remaining behaviors do not change the contents of the bag. One of these behaviors counts the number of times a given object occurs within the bag. Its specification in pseudocode is

```
// Counts the number of times a given entry appears in the bag.
getFrequencyOf(anEntry: ItemType): integer
```

Another method tests whether the bag contains a given object. We specify it in pseudocode as follows:

```
// Tests whether the bag contains a given entry.
contains(anEntry: ItemType): boolean
```

Finally, we want to look at the contents of the bag. Rather than providing a method that displays the entries in the bag, we will define one that places these entries into a vector. The client is then free to display any or all of them in any way desired. Here is the specification for our last method.

```
// Gets all entries in the bag.
toVector(): vector
```

As we developed the previous specifications for the bag's methods, we represented them using UML notation. Figure 1-7 shows the result of doing so.

## FIGURE 1-7 UML notation for the class Bag

| Bag |
| :--- |
| +getCurrentSize(): integer |
| +isEmpty(): boolean |
| +add(newEntry: ItemType): boolean |
| +remove(anEntry: ItemType): boolean |
| +clear(): void |
| +getFrequencyOf(anEntry: ItemType): integer |
| +contains(anEntry: ItemType): boolean |
| +toVector(): vector |

Notice that the CRC card and UML diagram do not reflect all of the details, such as assumptions and unusual circumstances. However, after you have identified such conditions, you should specify how your methods will behave under each one. You should write down your decisions about how you want your methods to behave, as we have done in the following table. Later, you can incorporate these informal descriptions into the C++ comments that document your methods.

## ABSTRACT DATA TYPE: BAG

- A finite number of objects, not necessarily distinct, in no particular order, and having the same data type.
- The number of objects in this collection.

| Pseudocode | Description |
| --- | --- |
| getCurrentSize() | Task: Reports the current number of objects in this bag. Input: None. Output: The number of objects currently in the bag. |
| isEmpty() | Task: Sees whether this bag is empty. Input: None. Output: True or false according to whether the bag is empty. |
| add(newEntry) | Task: Adds a given object to this bag. Input: newEntry is an object. Output: True or false according to whether the addition succeeds. |
| remove(anEntry) | Task: Removes an occurrence of a particular object from this bag, if possible. Input: anEntry is an object. Output: True or false according to whether the removal succeeds. |
| clear() | Task: Removes all objects from this bag. Input: None. Output: None. |
| getFrequencyOf(anEntry) | Task: Counts the number of times an object occurs in this bag. Input: anEntry is an object. Output: The integer number of times anEntry occurs in the bag. |
| contains(anEntry) | Task: Tests whether this bag contains a particular object. Input: anEntry is an object. Output: True or false according to whether anEntry occurs in the bag. |
| toVector() | Task: Gets all objects in this bag. Input: None. Output: A vector containing all entries currently in the bag. |

Note: Dealing with unusual conditions

As mentioned earlier, you must make decisions about how to treat unusual conditions. The documentation for the ADT bag should reflect both these decisions and the details in the previous discussion. For example, our specification of the method remove indicates that it will return false if a client tries to remove an entry from an empty bag. Instead, we could have given the method the precondition that the bag not be empty. It is then up to the client to check that the precondition is satisfied before invoking the method. Notice that the client can use other methods of the ADT bag, such as isEmpty and getCurrentSize, to help with this task.

Note: A first draft of an ADT's specifications often overlooks or ignores situations that you really need to consider. You might intentionally make these omissions to simplify this first draft. Once you have written the major portions of the specifications, you can concentrate on the details that make the specifications complete.

Question 1 Write specifications using UML notation for a function that computes the sum of the first five positive integers in an array of n arbitrary integers.

## 1.5.3 An Interface Template for the ADT

As your specifications become more detailed, they increasingly should reflect your choice of programming language. Ultimately, you can write C++ headers for the bag's methods and organize them into a header file for the class that will implement the ADT.

The C++ header file in Listing 1-1 contains the methods for an ADT bag and detailed comments that describe their behaviors. If you are unfamiliar with C++ classes, templates, and virtual methods, C++ Interlude 1 provides a refresher on C++ classes and discusses C++ templates, virtual methods, and abstract base classes. By using templates and abstract base classes, we can take advantage of the object-oriented design concepts of encapsulation, polymorphism, and inheritance beginning with our first ADT.

Note: To emphasize the distinction between the design of an ADT and its implementation with a data structure, this textbook uses templates and abstract base classes in the description of our ADTs. We will call the header file containing the abstract base class a client interface. A programmer should not need anything more than the client interface to use a class in your program, as it completely specifies the methods of the ADT.

As you examine the interface in Listing 1-1, notice the decisions that were made to address the unusual situations mentioned in the previous section. In particular, each of the methods add, remove, and contains returns a value. Note the commenting tags, which begin with @ and are described in Appendix I, that we use to specify the methods.

For now, the items in the bag will be objects of the same class. To accommodate entries of any single class type, the bag methods use a generic type ItemType for each entry. To give meaning to the identifier ItemType, we must write template<class ItemType> on the line before the class header. Once the actual data type is chosen by a client, the compiler will use that data type wherever ItemType appears.

The class BagInterface is a C++ abstract base class. An abstract base class, or simply an abstract class, in C++ contains at least one method that is declared as virtual and has no implementation. An abstract class cannot be instantiated; it can only be used as a base class. The subclass must then implement the methods specified but not defined in the abstract class.

```
LISTING 1-1 A file containing a C++ interface for bags

/** @file BagInterface.h */
#ifndef BAG_INTERFACE
#define _BAG_INTERFACE
#include <vector>

template<class ItemType>
class BagInterface
{
public:
//# Gets the current number of entries in this bag.
//@return The integer number of entries currently in the bag. */
virtual int getCurrentSize() const = 0;

//# Sees whether this bag is empty.
//@return True if the bag is empty, or false if not. */
virtual bool isEmpty() const = 0;

//# Adds a new entry to this bag.
//@post If successful, newEntry is stored in the bag and
// the count of items in the bag has increased by 1.
//@param newEntry The object to be added as a new entry.
//@return True if addition was successful, or false if not. */
virtual bool add(const ItemType& newEntry) = 0;

//# Removes one occurrence of a given entry from this bag,
// if possible.
//@post If successful, anEntry has been removed from the bag
// and the count of items in the bag has decreased by 1.
//@param anEntry The entry to be removed.
//@return True if removal was successful, or false if not. */
virtual bool remove(const ItemType& anEntry) = 0;

//# Removes all entries from this bag.
//@post Bag contains no items, and the count of items is 0. */
virtual void clear() = 0;

//# Counts the number of times a given entry appears in bag.
//@param anEntry The entry to be counted.
//@return The number of times anEntry appears in the bag. */
virtual int getFrequencyOf(const ItemType& anEntry) const = 0;
(continues)
```
