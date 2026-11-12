Programming Tip: When defining a class, implement and test a group of core methods. Begin with methods that add to a container of objects and/or have involved implementations.

# 3.1.2 Using Fixed-Size Arrays

When implementing an ADT that represents a data collection, you need to store the data items and track their number. In an **array-based implementation**, you store the items in an array. How much of the array will the items occupy? Possibly all of it, but this is not likely. That is, you need to keep track of the array elements that you have assigned to contain data and those that are available for use in the future. The maximum length of the array—its physical size—is a known, fixed value such as MAX_SIZE. You can keep track of the current number of items in the collection—that is, the collection’s logical size—in a variable. An obvious benefit of this approach is that implementing an operation that reports this value will be easy.

When you add a first entry to an array, you typically place it in the array’s first element—that is, the element whose index is 0. Doing so, however, is not a requirement, especially for arrays that implement containers. For example, some container implementations can benefit by ignoring the array element whose index is 0 and using index 1 as the first element in the array. Sometimes you might want to use the elements at the end of the array before the ones at its beginning. For the ADT bag, we have no reason to be atypical, and so the objects in a bag can begin at index 0 of the array.

Another consideration is whether the container’s entries should occupy consecutive elements of the array. Requiring the add method to place objects into an array contiguously is certainly reasonable, but why should we care, and is this really a concern? It is a concern, because we need to establish certain truths, or **assertions**, about our planned implementation so that the action of each method is not detrimental to other methods. For example, the method toVector must “know” where add has placed the entries. Our decision now also will affect what must happen later when we remove an entry from the container. If we insist that the bag’s entries occupy consecutive array elements, will the method remove ensure that they remain so?

What happens after add places a new entry into the last available array element? A subsequent addition will be impossible unless an entry is first removed from the array. An add method that encounters a full array should either signal its client or allocate a larger array. In this chapter, add will return a boolean value to indicate whether it was successful. In C++ Interlude 2, which follows this chapter, you will learn how to resize the array. Rather than returning a value, a method can signal its client by throwing an exception. C++ Interlude 3 will discuss this approach.

![](bbox=[0.1, 0.68, 0.2, 0.75])

# 3.2 An Array-Based Implementation of the ADT Bag

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