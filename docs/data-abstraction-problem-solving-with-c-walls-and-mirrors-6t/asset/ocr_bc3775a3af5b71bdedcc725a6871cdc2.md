```
{
   int frequency = 0;
   int curIndex = 0; // Current array index
   while (curIndex < itemCount)
   {
      if (items[curIndex] == anEntry)
      {
         frequency++;
      } // end if
   }
   curIndex++; // Increment to next entry
   } // end while
   return frequency;
} // end getFrequencyOf
```

**The method contains.** One easy way to define the method contains is to have it call the method getFrequencyOf, which we just defined. If the frequency of occurrence of a given entry is greater than zero, the bag must contain that entry. If the frequency is zero, the bag does not contain the entry. Thus, you could define contains as follows:

```
template<class ItemType>
bool ArrayBag<ItemType>::contains(const ItemType& target) const
{
   return getFrequencyOf(target) > 0;
} // end contains
```

Although this method will work, it usually will do more work than necessary. After all, getFrequencyOf must check every entry in the bag, whereas contains could quit looking at entries as soon as it finds one that is the same as the given entry. That is, its logic can be described by the following pseudocode:

```
contains(anEntry)
while (anEntry is not found and we have more array elements to check)
{
   if (anEntry equals the next array entry)
      anEntry is found in the array
}
```

This loop terminates under one of two conditions: Either anEntry has been found in the array or the entire array has been searched without success.

Based on this pseudocode, a definition of the method contains follows:

```
template<class ItemType>
bool ArrayBag<ItemType>::contains(const ItemType& anEntry) const
{
   bool found = false;
   int curIndex = 0; // Current array index
   while (!found && (curIndex < itemCount))
   {
      if (anEntry == items[curIndex])
      {
         found = true;
      } // end if
   }
   curIndex++; // Increment to next entry
   } // end while
   return found;
} // end contains
```