
FIGURE 3-5 (a) A gap in the array items after deleting the entry in items[index] and decrementing itemCount; (b) shifting subsequent entries to avoid a gap; (c) the array after shifting

![](img/288a0c22d14d2450c1e772f228f867b0_134_0.png)

Now consider how to remove the located item from the array. You could blank it out, but this strategy can lead to gaps in the array, as Figure 3-5a illustrates. An array that is full of gaps has three significant problems:

- itemCount - 1 is no longer the index of the last item in the array. You would need another variable, lastPosition, to contain this index.
- Because the items are spread out, the method contains might have to look at every element of the array, even when only a few items are present.
- When items[maxItems - 1] is occupied, the bag could appear full, even when fewer than maxItems items are present.

We could get rid of that gap by copying each successive entry to the previous element in the array, beginning with the entry after the removed item and ending with the last entry, as shown in Figure 3-5b. The result of shifting these entries is shown in Figure 3-5c. This time-consuming approach is not necessary, however.

Remember that we are not required to maintain any particular order for a bag's entries. So instead of shifting entries after removing an entry, we can replace the entry being removed with the last entry in the array, as follows. After locating anEntry in items[index], as Figure 3-6a indicates, we copy the entry in items[itemCount - 1] to items[index] (Figure 3-6b). We then ignore the entry in items[itemCount - 1] by decrementing itemCount.

The following pseudocode details the steps needed to remove a given entry from a bag. Note that by decrementing itemCount before using it in an index, we compute itemCount - 1 once instead of twice.

```
Search the array items for anEntry
if (anEntry is in the bag at items[index])
{
    Decrement the counter itemCount
    items[index] = items[itemCount]
    return true
}
else
return false
```

The initial search for anEntry is the same search as done in the method contains. Calling contains here is not much help, as we want to know not only whether the bag contains anEntry but also, if it does, where it occurs in the array. Clearly, we could modify the loop in contains slightly, but a better way places the loop in a private method that both contains and remove can call. This method is getIndexOf, which we declared earlier in the header file and whose definition follows:

```
template<class ItemType>
int ArrayBag<ItemType>::getIndexOf(const ItemType& target) const
{
   bool found = false;
   int result = -1;
   int searchIndex = 0;
   // If the bag is empty, itemCount is zero, so loop is skipped
   while (!found && (searchIndex < itemCount))
   {
      if (items[searchIndex] == target)
      {
         found = true;
         result = searchIndex;
      }
      else
      {
         searchIndex++;
      }  // end if
   }  // end while
   return result;
}  // end getIndexOf
```

FIGURE 3-6 Avoiding a gap in the array while removing an entry

![](img/288a0c22d14d2450c1e772f228f867b0_135_0.png)

The method remove now has the following definition:

```
template<class ItemType>
bool ArrayBag<ItemType>::remove(const ItemType& anEntry)
{
   int locatedIndex = getIndexOf(anEntry);
   bool canRemoveItem = !isEmpty() && (locatedIndex > -1);
   if (canRemoveItem)
   {
      itemCount--;
      items[locatedIndex] = items[itemCount];
   } // end if
   return canRemoveItem;
} // end remove
```

> **Programming Tip: Should the method getIndexOf be public or private?**
> 
> You might think that the method getIndexOf, since it returns the index of an entry in the array, entries, would be useful to a client. While that might be true, there are important reasons why the method should be private. We declared the array items as private because it is detail of our array-based implementation. The client cannot access the entries in this array without invoking a public method of our class. The indices of these entries are also implementation details that are of no use to the client because it cannot access the array items by name. Any method that returns an index to a private array should be declared as private.

- **Question 4** Revise the definition of the method contains so that it calls the method getIndexOf.
-
- **Question 5** Should we revise the specification of the method contains so that if it locates a given entry within the bag, it returns the index of that entry?
-
- **Question 6** Revise the definition of the method getIndexOf so that it does not use a boolean variable.

The method clear. The method clear can make a bag appear empty simply by setting itemCount to zero. Thus, we have the following definition for this method:

```
template<class ItemType>
void ArrayBag<ItemType>::clear()
{
   itemCount = 0;
} // end clear
```

## 3.2.6 Testing

To test our completed class, we can add the following statements to the method bagTester that appears in Listing 3-2:

```
cout << "contains(\"three\"): returns " << bag.contains("three")
     << "; should be 1 (true)" << endl;
cout << "contains(\"ten\"): returns " << bag.contains("ten")
     << "; should be 0 (false)" << endl;
cout << "getFrequencyOf(\"one\"): returns "
     << bag.getFrequencyOf("one") << " should be 2" << endl;
cout << "remove(\"one\"): returns " << bag.remove("one")
     << "; should be 1 (true)" << endl;
cout << "getFrequencyOf(\"one\"): returns "
     << bag.getFrequencyOf("one") << " should be 1" << endl;
cout << "remove(\"one\"): returns " << bag.remove("one")
     << "; should be 1 (true)" << endl;
cout << "remove(\"one\"): returns " << bag.remove("one")
     << "; should be 0 (false)" << endl;
displayBag(bag);
cout << "After clearing the bag, ";
bag.clear();
cout << "isEmpty: returns " << bag.isEmpty()
     << "; should be 1 (true)" << endl;
```

> Note: References such as bag.itemCount and bag.items[4] would be illegal within the client, because itemCount and items are within the private portion of the class.

> Note: To implement an ADT, given implementation-independent specifications of the ADT’s operations, you first must choose a data structure to contain the data. Next, you declare a class within a header file. The ADT’s operations are public methods within the class, and the ADT’s data consists of class members that are typically private. You then implement the class’s methods within an implementation file. The program that uses the class will be able to access the data only by using the ADT’s operations.

> Note: In practice, when choosing among implementations of an ADT, you must ask whether the fixed-sized restriction of an array-based implementation presents a problem in the context of a particular application. The answer to this question depends on two factors. The obvious factor is whether, for a given application, you can predict in advance the maximum number of items in the ADT at any one time. If you cannot, it is quite possible that an operation—and hence the entire program—will fail because the ADT in the context of a particular application requires more storage than the array can provide.
> 
> On the other hand, if for a given application you can predict in advance the maximum number of items in an ADT at any one time, you must explore a more subtle factor: Would you waste storage by declaring an array to be large enough to accommodate this maximum number of items? Consider a case in which the maximum number of items is large, but you suspect that this number rarely will be reached. For example, suppose that a bag can contain as many as 10,000 items, but the actual number of items in the bag rarely exceeds 50. If you declare 10,000 array locations at compilation time, at least 9,950 array locations will be wasted most of the time.
> 
> We can avoid both of the previous cases by allocating a larger—or smaller—array during execution. The next C++ Interlude will show you how.
