# An Array-Based Implementation of the ADT Bag

```
items[index] = items[itemCount]
return true
}
else
  return false
```

The initial search for anEntry is the same search as done in the method contains. Calling contains here is not much, as we want to know not whether the bag contains anEntry but also if, where it occurs in the array. Clearly, we could modify the loop slightly slightly, but a better way places the loop in a private method that contains remove and can call: This method is getIndexOfOf, which we declared earlier in the header file and with definition follows:

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
    } // end if
  } // end while
  return result;
} // end getIndexOf
```

FIGURE 3-6 Avoiding a gap in the array while removing an entry

![](bbox=[0.134, 0.642, 0.856, 0.903])