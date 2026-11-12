
An ADT is a collection of data and a set of operations on that data

Specifications indicate what ADT operations do, but not how to implement them

## 3.1 The Approach

We have said that a collection of data, together with a set of operations on that data, are called an abstract data type, or ADT. For example, suppose that you want to store a collection of names that you can search rapidly. The collection of names, together with operations that add a name, remove a name, and search for a name, can form an ADT that solves this problem.

Previously, we emphasized the specification of an abstract data type. When you design an ADT, you concentrate on what its operations do, but ignore how you will implement them. That is, the description of an ADT's operations must be rigorous enough to specify completely their effect on the data, yet must not specify how to store the data nor how to carry out the operations. For example, the operations of an ADT should not specify whether to store the data in consecutive memory locations or in disjoint memory locations. The result should be a set of clearly specified ADT operations.

How do you implement an ADT once its operations are clearly specified? That is, how do you store the ADT's data and carry out its operations? You begin by choosing particular data structures to store the data. Recall that a data structure is a construct that you can define within a programming language to store a collection of data. For example, C++ arrays are data structures.

Your first reaction to the implementation question might be to choose a data structure and then to write functions that access it in accordance with the ADT's operations. Although this point of view is not incorrect, hopefully you have learned not to jump right into code. In general, you should refine an ADT through successive levels of abstraction yielding successively more concrete descriptions of the ADT.

The choices that you make during the implementation process can affect the execution time of your code. For now, our analyses will be intuitive, but Chapter 10 will introduce you to quantitative techniques that you can use to weigh the trade-offs involved.

Recall that the client—that is, the program that uses the ADT—should see only a wall of available operations that act on data, as Figure 1-5 in Chapter 1 illustrates. Both the data structure that you choose to contain the data and the implementations of the ADT's operations are hidden behind the wall. By now, you should realize the advantage of this wall and take steps to prevent a client's direct access—either intentional or accidental—to the data structure, as shown in Figure 3-1. Why is such access undesirable? Public data fields allow the client to go around the wall of abstraction and access the ADT's data directly. For example, suppose that you use an array items to store an ADT's data. In a program that uses the ADT, you might, for example, accidentally access the first element in the array by writing

```
firstItem = items[0];
```

instead of by invoking an ADT operation. If you changed to another implementation of the ADT, your program would be incorrect. To correct your program, you would need to locate and change all occurrences of items[0]—but first you would have to realize that items[0] is in error! Moreover, by violating the wall, a client could damage the ADT's data. If the data were ordered in a certain way, for example, the ADT's operations would ensure that the order was maintained. But if a client could alter the data directly, that order could be destroyed.

> Note: Implementing an ADT as a C++ class provides a way for you to enforce the wall of an ADT, thereby preventing access of the data structure in any way other than by using the ADT's operations. A client then cannot damage the ADT's data. Moreover, the client is independent of the details of the ADT's implementation, because it adheres only to the ADT's specifications.

### FIGURE 3-1 Violating the wall of ADT operations

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_123_0.png)

### 3.1.1 Core Methods

The definition of a class that implements an ADT could be fairly involved. In general, you should not define the entire class and then attempt to test it. Instead, you should identify a group of core methods to both implement and test before continuing with the rest of the class definition. By leaving the definitions of the other methods for later, you can focus your attention and simplify your task. But what methods should be part of this group? In general, such methods should be central to the purpose of the class and allow reasonable testing. We sometimes will call a group of core methods a core group.

When dealing with a container such as a bag, for example, you cannot test most methods until you have created the container and placed items into it. Thus, adding objects to the container is a fundamental operation. If the method add does not work correctly, testing other methods such as remove would be pointless. Thus, the add method would be part of the group of core methods that we implement first.

To test whether add works correctly, we need a method that allows us to see the container's data. For the ADT bag, the method toVector serves this purpose, and so it is a core method. Any constructors are also fundamental and are in the core group. Similarly, other methods that a core method might call are part of the core group as well. Such methods might be public methods within the ADT or private “helper” methods.

> Note: Methods such as add and remove that can alter the underlying data structure of a container are likely to have the most involved implementations. In general, you should define such methods before the others in the class. But since you cannot test remove before add is correct, you should delay implementing it until after add is completed and thoroughly tested.

Programming Tip: When defining a class, implement and test a group of core methods. Begin with methods that add to a container of objects and/or have involved implementations.

### 3.1.2 Using Fixed-Size Arrays

When implementing an ADT that represents a data collection, you need to store the data items and track their number. In an **array-based implementation**, you store the items in an array. How much of the array will the items occupy? Possibly all of it, but this is not likely. That is, you need to keep track of the array elements that you have assigned to contain data and those that are available for use in the future. The maximum length of the array—its physical size—is a known, fixed value such as MAX_SIZE. You can keep track of the current number of items in the collection—that is, the collection’s logical size—in a variable. An obvious benefit of this approach is that implementing an operation that reports this value will be easy.

When you add a first entry to an array, you typically place it in the array’s first element—that is, the element whose index is 0. Doing so, however, is not a requirement, especially for arrays that implement containers. For example, some container implementations can benefit by ignoring the array element whose index is 0 and using index 1 as the first element in the array. Sometimes you might want to use the elements at the end of the array before the ones at its beginning. For the ADT bag, we have no reason to be atypical, and so the objects in a bag can begin at index 0 of the array.

Another consideration is whether the container’s entries should occupy consecutive elements of the array. Requiring the add method to place objects into an array contiguously is certainly reasonable, but why should we care, and is this really a concern? It is a concern, because we need to establish certain truths, or **assertions**, about our planned implementation so that the action of each method is not detrimental to other methods. For example, the method toVector must “know” where add has placed the entries. Our decision now also will affect what must happen later when we remove an entry from the container. If we insist that the bag’s entries occupy consecutive array elements, will the method remove ensure that they remain so?

What happens after add places a new entry into the last available array element? A subsequent addition will be impossible unless an entry is first removed from the array. An add method that encounters a full array should either signal its client or allocate a larger array. In this chapter, add will return a boolean value to indicate whether it was successful. In C++ Interlude 2, which follows this chapter, you will learn how to resize the array. Rather than returning a value, a method can signal its client by throwing an exception. C++ Interlude 3 will discuss this approach.

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_124_0.png)

## 3.2 An Array-Based Implementation of the ADT Bag

We will now make the previous discussion concrete by implementing the ADT bag as a class using an array to store its entries. Recall from Chapter 1 that the ADT bag’s operations are

```
+getCurrentSize(): integer
+isEmpty(): boolean
+add(newEntry: ItemType): boolean
+remove(anEntry: ItemType): boolean
+clear(): void
+getFrequencyOf(anEntry: ItemType): integer
+contains(anEntry: ItemType): boolean
+toVector(): vector
```

These operations will become public methods in our class. Each method will require access to both the array of bag entries and the current number of entries in the bag. Thus, we make the array and a counter data members of the class. Since the length of the
