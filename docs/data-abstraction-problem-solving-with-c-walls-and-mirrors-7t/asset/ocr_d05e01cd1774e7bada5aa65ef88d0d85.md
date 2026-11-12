# 4.2.3 Implementing More Methods

Having successfully defined the core methods, we will continue to define the remaining ones in our class.

**The method** getFrequencyOf. To count the number of times a given object occurs in a bag, we count the number of times the object occurs in the linked chain. To do so, we need to traverse the chain and compare each of its data items with the given object. Each time we find a match, we increment a counter. When the traversal ends, we return the value of the counter.

The loop we will use is like the one we wrote in the method toVector. Here is the definition of getFrequencyOf:

```
template<class ItemType>
int LinkedBag<ItemType>::getFrequencyOf(const ItemType& anEntry) const
{
   int frequency = 0;
   int counter = 0;
   Node<ItemType>* curPtr = headPtr;
   while ((curPtr != nullptr) && (counter < itemCount))
   {
      if (anEntry == curPtr->getItem())
      {
         frequency++;
      } // end if

      counter++;
      curPtr = curPtr->getNext();
   } // end while

   return frequency;
} // end getFrequencyOf
```

![](bbox=[0.06, 0.54, 0.1, 0.59])

**Question 4** Suppose that the ADT bag had an operation that displayed its contents. Write a C++ definition for such a method for the class LinkedBag.

**Question 5** How many assignment operations does the method that you wrote for the previous question require?

**The method** contains. The discussion in Chapter 3 about the method contains applies here as well. Although the method could call the method getFrequencyOf, which we just defined, doing so usually will involve more work than is necessary. Whereas getFrequencyOf must check every entry in the bag, contains exits as soon as it finds an entry in the bag that is the same as the given one.

We observed in the previous chapter that the methods contains and remove perform the same search for a specific entry. Thus, to avoid duplicate code, we perform this search in a private method that both contains and remove can call. We declared this private method in the header file, and its definition follows.

// Returns either a pointer to the node containing a given entry // or the null pointer if the entry is not in the bag.

```
template<class ItemType>
Node<ItemType>* LinkedBag<ItemType>::getPointerTo(const ItemType& target) const
{
   bool found = false;
   Node<ItemType>* curPtr = headPtr;
```