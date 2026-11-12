The method remove. Now consider how to remove an entry from the list. You could blank it out, but this strategy can lead to gaps in the array, as Figure 9-3a illustrates. An array that is full of gaps has three significant problems:

+   - itemCount – 1 is no longer the index of the last entry in the array. You need another variable, lastPosition, to contain this index.
+   - Because the items are spread out, the method getEntry might have to look at every cell of the array even when only a few entries are present.
+   - When items[maxItems - 1] is occupied, the list could appear full, even when fewer than maxItems entries are present.

Thus, what you really need to do is shift the entries in the array so that a deletion does not leave a gap, as shown in Figure 9-3b. This data movement is like the one done by the method insert, but it occurs in the opposite direction.

The definition of remove follows:

```
```cpp
template<class ItemType>
bool ArrayList<ItemType>::remove(int position)
{
   bool ableToRemove = (position >= 1) && (position <= itemCount);
   if (ableToRemove)
   {
      // Remove entry by shifting all entries after the one at
      // position toward the beginning of the array
      // (no shift if position == itemCount)
      for (int fromIndex = position, toIndex = fromIndex - 1;
           fromIndex < itemCount; fromIndex++, toIndex++)
         items[toIndex] = items[fromIndex];
      itemCount--; // Decrease count of entries
   } // end if

   return ableToRemove;
} // end remove
```
```

# FIGURE 9-3 (a) Deletion can cause a gap; (b) shift items to prevent a gap at position 3; (c) the result

![](bbox=[0.06, 0.62, 0.92, 0.73])

![](bbox=[0.06, 0.74, 0.92, 0.82])

![](bbox=[0.06, 0.83, 0.92, 0.92])