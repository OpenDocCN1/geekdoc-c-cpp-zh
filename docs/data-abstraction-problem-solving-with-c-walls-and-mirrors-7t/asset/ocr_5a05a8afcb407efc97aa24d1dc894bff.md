```
{
   int newPosition = fabs(getPosition(newEntry));
   listPtr->insert(newPosition, newEntry);
} // end insertSorted
```

**The method removeSorted.** The method removeSorted can call getPosition to determine where in the sorted list the given entry exists or belongs. This time, however, we do need to know whether the entry exists in the list. If it does not exist, we cannot remove it, so removeSorted will return false when this is the case. Otherwise, the returned position will be positive, and removeSorted can call the list's method remove to delete the entry. We leave the implementation of removeSorted to you in Checkpoint Question 11.

**The method getPosition.** Implementing getPosition is somewhat harder than implementing the previous two methods. To decide where in a sorted list an entry is or belongs, we need to compare it to the entries already in the list, beginning with the first one. If the given entry is in the list, we obviously compare entries until we find a match. However, if it is not in the list, we want to stop the search at the point where it belongs in the sorted list. We take advantage of the sorted order of the objects by using logic similar to that described in Section 12.2.2.

Checkpoint Question 12 asks you to define getPosition. You can do so by using the methods getLength and getEntry.

![](bbox=[0.22, 0.41, 0.28, 0.46])

**Question 9** Repeat Checkpoint Question 7 using the method insertSorted of the class SortedListHasA.

**Question 10** Can a client of SortedListHasA invoke the method insert of the ADT list? Explain.

**Question 11** Define the method removeSorted for the class SortedListHasA.

**Question 12** Define the method getPosition for the class SortedListHasA.

**The remaining methods.** Each of the methods isEmpty, getLength, remove, clear, and getEntry of the ADT sorted list has the same specifications as in the ADT list. Each can simply invoke the corresponding list method. For example, the method remove has the following implementation in SortedListHasA:

```
template<class ItemType>
bool SortedListHasA<ItemType>::remove(int position)
{
   return listPtr->remove(position);
} // end remove
```

**Efficiency issues.** Except perhaps for some subtle logic in getPosition, you can write the previous implementation quickly and with few, if any, errors. Saving human time is an attractive feature of using an existing class to build another. But does the implementation use computer time efficiently? In this particular implementation, several methods invoke getPosition, so their efficiency depends on getPosition's efficiency.

The method getPosition calls the list method getLength, which is an O(1) operation. Therefore, we need not be concerned with it. On the other hand, a loop examines the entries in the list one at a time by invoking getEntry until the desired entry is located. Thus, the efficiency of getPosition depends in part on the efficiency of getEntry. However, the efficiency of getEntry depends upon which implementation of the ADT list you use. For the link-based implementation, getEntry is O(n). Since getPosition invokes getEntry within a loop, getPosition is O(n^2) in the worst case. Note that each time getEntry retrieves the next entry in the list, it starts its search at the beginning of the chain. This is the cause of getPosition's inefficiency.