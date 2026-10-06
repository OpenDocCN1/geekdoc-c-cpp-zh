```
{
  itemCount = 0;
  maxItems = DEFAULT_CAPACITY;
} // default constructor
```

Although you can simply use an assignment statement to assign a value to a data member, as we have done here, it is preferable to use an initializer. Each initializer uses a functional notation that consists of a data member name followed by its initial value in parentheses—for example, itemCount(0). If you have more than one, you separate them with commas. A colon precedes the first (or only) initializer. Thus, a better definition of ArrayBag's constructor is

```
template<class ItemType>
ArrayBag<ItemType>::ArrayBag(itemCount(0), maxItems(DEFAULT_CAPACITY))
{
// default constructor
```

The implementation of a constructor consists only of initializers, unless its body is, as is the case here. Note that you can use these initializers for constructors but with other methods.

> **Programming Tip:** When a class has several data members, the constructor initializes them in the order in which they appear in the class definition instead of the order in which the initializers appear in the constructor definition. You should use the same order in both cases to avoid confusion, even if the initializer order does not make a difference.

**The add method.** To add a new item to a bag that is not full, we can place it right after the last item in the array by writing the following statement:

```
items[itemCount] = newEntry;
```

If we are adding to an empty bag, itemCount will be zero, and the assignment will be to items[0]. If the bag contains one entry, an additional entry will be assigned to items[1], and so on. In this way, no other items in the array need to move. After each addition, we increase the counter itemCount. Figure 3-3 depicts this insertion. If add succeeds, it returns true. Otherwise—if the bag is full, it returns false, as you can see from its definition:

```
template<class ItemType>
bool ArrayBag<ItemType>::add(const ItemType& newEntry)
{
  bool hasRoomToAdd = (itemCount < maxItems);
  if (hasRoomToAdd) {
    items[itemCount] = newEntry;
    itemCount++;
  }
  return hasRoomToAdd;
}
```

> Note: The entries in a bag have no particular order. Thus, the add method can place a new entry into any convenient element of the array items. In the previous definition of add, that element is the one immediately after the last element used.