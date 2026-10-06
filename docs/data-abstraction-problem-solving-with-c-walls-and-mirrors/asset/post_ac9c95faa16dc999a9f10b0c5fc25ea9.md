
## 9.1.2 The Implementation File

![](img/d0cb86b2f18b2db569968ad7c743510e_294_0.png)

Overview of ArrayList

As usual, we will begin our implementation with the method or methods that add new entries to our container and any methods that help us to verify the correctness of those additions. For ArrayList, we will define the insert method. The methods isEmpty and getLength will be easy to define and use while testing insert. We also want to call the method getEntry to check the contents of the list. And, of course, we need to define the constructor. Let's begin with these methods as our core group.

The constructor and the methods isEmpty and getLength. The default constructor initializes the data members itemCount to zero and maxItems to DEFAULT_CAPACITY:

```cpp
template<class ItemType>
ArrayList<ItemType>::ArrayList() : itemCount(0)
{
    maxItems =DEFAULT_CAPACITY);
} // end constructor
```

The method isEmpty tests whether itemCount is zero, and getLength returns the value of itemCount:

```cpp
template<class ItemType>
bool ArrayList<ItemType>::isEmpty() const
{
    return itemCount == 0;
} // end isEmpty
```

```cpp
template<class ItemType>
int ArrayList<ItemType>::getLength() const
{
    return itemCount;
} // end getLength
```

To insert a new entry at a given position in the array items, you must create room for the new entry by shifting the entries at that position toward the end of the array. Figure 9-2 depicts this insertion. Part (a) shows the list prior to adding a new entry at position 3. Starting from the end of the list, we copy the entry in items[i-1] to items[i] for values of i ranging from k down to 3, as Figure 9-b illustrates. Finally, we insert the new entry into items[newPosition - 1], or items[i] after this step. Figure 9-c shows the list after the method insert.

The definition of the insert method follows:

```cpp
template<class ItemType>
bool ArrayList<ItemType>::insert(int newPosition,
                               const ItemType&newEntry)
{
    bool ableToInsert = (newPosition >= 0) &&
                        (newPosition <= itemCount + 1) &&
                        (itemCount < maxItems);
    if (ableToInsert)
    {
        // Make room for new entry by shifting all entries at
        // positions >= newPosition toward the end of the array
        // (no shift if itemCount == position - 1)
        for (int pos = itemCount; pos >= newPosition; pos--)
            items[pos] = items[pos - 1];

        // Insert new entry
        items[newPosition - 1] = newEntry;
        itemCount++; // Increase count of entries
    }
    return ableToInsert;
} // end insert
```

Shift array entries to insert an item

![](img/d0cb86b2f18b2db569968ad7c743510e_294_1.png)

# An Array-Based Implementation of the ADT

FIGURE 9-2 Shifting items for insertion: (a) the list before the insertion; (b) copy items to produce room at position 3; (c) the result

![](img/d0cb86b2f18b2db569968ad7c743510e_295_0.png)

We can begin testing these methods once we write stubs for the remaining methods. To thoroughly test insert, however we need the method getEntry, which we define next.

**Question 1** Given a nonempty list that is an instance of ArrayList, at what position does an insertion of a new entry require the following operations?

**Question 2** Describe an implementation of the method insert for ArrayList that places the entry in position 1 in the last element of the array, the entry in position 2 in the next-to-last element, and so on.

**Question 3** How does the original version of insert given previously compare with the one described in Question 2 with respect to the number of operations required?

**The method getEntry.** This simple method needs to return the value in items[position], but we decided to enforce the method's precondition by throwing an exception if the position is out of bounds. For the purpose of testing the method insert, you could write a temporary version of getEntry that does not throw an exception but just returns the list entry. You dont complete its definition as follows:

```cpp
template<class ItemType>
ItemType ArrayList<ItemType>::getEntry(int position) const
throw(PreconditionViolatedException)
```

```cpp
{
    // Enforce precondition
    bool ableToGet = (position >= 1) && (position <= itemCount);
    if (ableToGet) {
        return items[position - 1];
    } else {
        string message = "getEntry() called with an empty list or ";
        message = message + "invalid position.";
        throw(PreconditionViolatedException(message));
    }
} // end getEntry
```

A client. At this point, and after writing stubs for the remaining methods, you should test the core group of methods. The following main function demonstrates how you can test the insert and getEntry, and whether it changes the value of DEFAULT_CAPACITY in List 9-1:

```cpp
int main() {
    List<string> listPtr = new ArrayList<string>();
    string data[] = {"one", "two", "three", "four", "five"};
    cout << "isEmpty: " << listPtr->isEmpty() << " (true)" << endl;
    for (int i = 0; i < 5; i++) {
        if (listPtr->insert(i + 1, data[i]))
            cout << "Inserted " << listPtr->getEntry(i + 1) << endl;
        else
            cout << "Cannot insert " << data[i] << " at position " << (i + 1) << endl;
    }
    return 0;
} // end main
```

A client of the class cannot access the class's private members directly. Note that code write references to listPtr->itemCount or listPtr->items[i], because itemCount and items are within the private partition of the class.

The method setEntry. The definition of the method setEntry is similar to getEntry, so we implement it:

```cpp
template<class ItemType>
void ArrayList<ItemType>::setEntry(int position, const ItemType& newEntry)
throw(PreconditionViolatedException)
{
    // Enforce precondition
    bool ableToSet = (position >= 1) && (position <= itemCount);
    if (ableToSet) {
        items[position - 1] = newEntry;
    } else {
        string message = "setEntry() called with an empty list or ";
        message = message + "invalid position.";
        throw(PreconditionViolatedException(message));
    }
} // end setEntry
```

# An Array-Based Implementation of the ADT

The method remove. Now consider to remove an entry from a list. You could blank it out, but this strategy can lead to gaps in the array, as Figure 9-3 illustrates. An array that is full of gaps has three problems:

- itemCount is no longer the index of the last entry in the array. You need another variable, lastPosition, to contain this.
- Because the entries are erased, the method getEntry might have to look at every cell of the array even when a few entries are present.
- When items[maxItems - 1] is occupied, the list could appear full, even when fewer than maxItems entries are present.

Thus, you will really need to shift entries in the array so that a deletion does not leave a gap, as shown in Figure 9-3. This data movement is the one done by the method insert, but it occurs in the opposite direction.

The definition follows:

```cpp
template<class ItemType>
bool ArrayList<ItemType>::remove(int position)
{
    bool ableToRemove = (position >= 1) && (position <= itemCount);
    if (ableToRemove) {
        // shifting all entries after the one at
        // position toward the beginning of the array
        // (no shift if position == itemCount)
        for (int from = position, to = itemCount - 1; from < itemCount; from++, to++)
            items[to] = items[from];
        itemCount--; // Decrease count of entries
    }
    return ableToRemove;
} // end remove
```

![](img/d0cb86b2f18b2db569968ad7c743510e_297_0.png)

The method clear. To clear all the entries from a list, our final method simply sets itemCount to zero.

```cpp
template<class ItemType>
void ArrayList<ItemType>::clear()
{
    itemCount = 0;
} // end clear
```

The entire implementation file for the class ArrayList is available online from the book's website.

> Question 4 Although the method cannot remove an entry from an empty list, it does not explicitly check for one. How does this method avoid deletion from an empty list?

## 9.2 A Link-Based Implementation of the ADT List

We now consider how to use C++ pointers instead of an array to implement the ADT list. Unlike the array-based implementation, a link-based implementation does not shift items during insertion and deletion operations. It also does not fix a maximum length on the list—except, of course, as imposed by the storage limits of the system. Once again, we need to represent the entries in the list. Listing 9-4 indicates one possible way to represent this data using pointers. Here headPtr points to the linked nodes containing the items in the list, where the first node contains the entry at position 1 in the list, and so on. The itemCount is the current number of entries in the list. Both headPtr and itemCount are private data members of our class.

### 9.2.1 The Header File

Let's name our class LinkedList and write its header file as shown in Listing 9-2. This file has similarities to the header file for ArrayList, as given in Listing 9-1, but let's point out the differences. Here we include the header files for the class Node and PrevalidatedException, as defined in Listing 4-1 of Chapter 4 and Listing 7-5 of Chapter 7, respectively.

The private section declares the two data members—headPtr and itemCount—as a private method getAt that we will use to locate any node within the chain of linked nodes, given its position in the chain. Unlike an array, which provides direct access to a specified element, the chain of linked nodes requires the insertion, and removal operations to traverse it until the specified node is reached. While you could write the necessary loop in the method getEntry, you would soon discover that the methods insert and remove will need the same loop. At that time, you should

FIGURE 9-4 A link-based implementation of the ADT list

![](img/d0cb86b2f18b2db569968ad7c743510e_298_0.png)
