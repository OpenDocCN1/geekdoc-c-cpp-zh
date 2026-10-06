# C++ INTERLUDE 2 Pointers, Polymorphism, and Memory Allocation

```
items = new ItemType[2 * maxItems];
for (int index = 0; index < maxItems; index++)
items[index] = oldArray[index];
delete[] items = 2 * maxItems;
// end if
// We can always add the item
```

```
items[itemCount] = newEntry;
itemCount++;
return true;
}// end ResizableArraybag
```

Doubling the array each time the bag is full is not as attractive as it might first seem. Each time you expand the size of an array, you copy the 50-element array to a 100-element array before completing the addition. When the array is a small 50-element array, 49 additions can be made quickly without copying the array.

If you have a 50,000-element array that is full, you must allocate memory for 100,000 entries before copying the 50,000 entries in the current array. This takes considerably longer to do and a significantly greater amount of memory. It is possible that you needed storage for only 50,001 entries and will have 49,999 unused array elements wasting memory. Once you realize that your array is too large, you could reduce its size by allocating a smaller array and copying the entries to this new array. However, there is no way to predict whether or not you should do so. The application might need the extra array elements in the future.

In Chapter 4, we consider another implementation of the ADT bag that does not have this memory-allocation problem and that never becomes full.