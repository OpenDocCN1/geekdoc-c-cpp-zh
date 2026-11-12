
### 1.5.1 Identifying Behaviors

Since a bag contains a finite number of objects, reporting how many objects it contains could be one of a bag’s behaviors:

- Get the number of items currently in the bag.

A related behavior detects if a bag is empty:

- See whether the bag is empty.

We should be able to add and remove objects:

- Add a given object to the bag.
- Remove an occurrence of a specific object from the bag, if possible.
- Remove all objects from the bag.

Note that the add operation does not indicate where in the bag an object should go. Remember that a bag does not order its contents. The remove operation looks for a particular item in the bag. If it finds it, it takes it out. If the bag contains several objects equal to the removed one, they remain in the bag. If the operation can’t find the specific object in the bag, it can’t remove it, and just says so. Finally, the second remove operation simply empties the bag of all objects.

What is in a particular bag? The answer to this question can be answered by the following operations:

- Count the number of times a certain object occurs in the bag.
- Test whether the bag contains a particular object.
- Look at all objects that are in the bag.

We have enough behaviors for now. At this point, we would have written all the behaviors on a piece of paper or, as Appendix C suggests, on the class-responsibility-collaboration (CRC) card pictured in Figure 1-6.

FIGURE 1-6 A CRC card for a Class Bag

| Bag |
| --- |
| Responsibilities |
| Get the number of items currently in the bag |
| See whether the bag is empty |
| Add a given object to the bag |
| Remove an occurrence of a specific object from the bag |
| Remove all objects from the bag |
| Count the number of times a certain object occurs in the bag |
| Test whether the bag contains a particular object |
| Look at all objects that are in the bag |
| Collaborations |
| The class of objects that the bag can contain |

Since a bag is an abstract data type, we only describe its data and specify its operations. We do not indicate how to store the data or how to implement its operations. Don't think about arrays, for example. You first need to clearly know what the bag operations do: Focus on what the operations do, not on how you do them. That is, you need a detailed set of specifications before you can use a bag in a program. In fact, you should specify the bag operations before you even decide on a programming language.

### 1.5.2 Specifying Data and Operations

Before we can implement a bag in C++, we need to describe its data and specify in detail the methods that correspond to the bag's behaviors. We'll name the methods, choose their parameters, decide their return types, and write comments to fully describe their effect on the bag's data. Our eventual goal, of course, is to write a C++ header file and comments for each method. However, we first will express the methods in pseudocode and then in UML notation.

The first behavior on our CRC card gives rise to a method that returns a count of the current number of entries in the bag. The corresponding method has no parameters and returns an integer. In pseudocode, we have the following specification, again using UML notation:

Use the UML to describe classes at various stages of their development

```
// Returns the current number of entries in the bag.
+getCurrentSize(): integer
```

We can test whether the bag is empty by using a boolean-valued method, again without parameters. Its specification in pseudocode is

```
// Returns true if the bag is empty.
+isEmpty(): boolean
```

We now want to add a given object to the bag. We can name the method add and give it a parameter to represent the new entry. We could write the following pseudocode:

```
// Adds a new entry to the bag.
add(newEntry)
```

We might be tempted to make add a void method, but if the bag is full, we cannot add a new entry to it. What should we do in this case? Here are two options that we can take when add cannot complete its task:

- Do nothing. We cannot add another item, so we ignore it and leave the bag unchanged.

- Leave the bag unchanged, but signal the client that the addition is impossible.

The first option is easy, but it leaves the client wondering what happened. Of course, we could state as a precondition of add that the bag must not already be full. Then the client has the responsibility to avoid adding a new entry to a full bag.

The second option is the better one, and it is not too hard to specify or implement. How can we indicate to the client whether the addition was successful? We could throw an exception if the addition is not successful, but we will leave this approach for later and use another way. Displaying an error message is not a good choice, as you should let the client dictate all written output. Since the addition is either successful or not, we can simply have the method add return a boolean value.

Thus, we can specify the method add more completely as

```
+add(newEntry: ItemType): boolean
```

where newEntry's data type is ItemType. In C++ Interlude 1, we will discuss the implementation details of using templates and typedef statements to give us flexibility in the type of data our ADT can hold.

Two behaviors involve removing entries from a bag: remove a particular entry and remove all entries. Suppose we name the methods and any parameters and begin to specify them in pseudocode as follows:

```
// Removes one occurrence of a particular entry from the bag, if possible.
remove(anEntry)
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

FIGURE 1-7 UML notation for the class Bag

| Bag |
| --- |
| +getCurrentSize(): integer |
| +isEmpty(): boolean |
| +add(newEntry: ItemType): boolean |
| +remove(anEntry: ItemType): boolean |
| +clear(): void |
| +getFrequencyOf(anEntry: ItemType): integer |
| +contains(anEntry: ItemType): boolean |
| +toVector(): vector |

Notice that the CRC card and UML diagram do not reflect all of the details, such as assumptions and unusual circumstances. However, after you have identified such conditions, you should specify how your methods will behave under each one. You should write down your decisions about how you want your methods to behave, as we have done in the following table. Later, you can incorporate these informal descriptions into the C++ comments that document your methods.

### ABSTRACT DATA TYPE: BAG

- Data
  - A finite number of objects, not necessarily distinct, in no particular order, and having the same data type.
  - The number of objects in this collection.

| Pseudocode | Description |
| :--- | :--- |
| getCurrentSize() | Task: Reports the current number of objects in this bag.<br>Input: None.<br>Output: The number of objects currently in the bag. |
| isEmpty() | Task: Sees whether this bag is empty.<br>Input: None.<br>Output: True or false according to whether the bag is empty. |
| add(newEntry) | Task: Adds a given object to this bag.<br>Input: newEntry is an object.<br>Output: True or false according to whether the addition succeeds. |
| remove(anEntry) | Task: Removes an occurrence of a particular object from this bag, if possible.<br>Input: anEntry is an object.<br>Output: True or false according to whether the removal succeeds. |
| clear() | Task: Removes all objects from this bag.<br>Input: None.<br>Output: None. |
| getFrequencyOf(anEntry) | Task: Counts the number of times an object occurs in this bag.<br>Input: anEntry is an object.<br>Output: The integer number of times anEntry occurs in the bag. |
| contains(anEntry) | Task: Tests whether this bag contains a particular object.<br>Input: anEntry is an object.<br>Output: True or false according to whether anEntry occurs in the bag. |
| toVector() | Task: Gets all objects in this bag.<br>Input: None.<br>Output: A vector containing all entries currently in the bag. |
