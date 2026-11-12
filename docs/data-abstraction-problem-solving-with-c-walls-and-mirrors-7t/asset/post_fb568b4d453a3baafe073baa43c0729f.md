
example, if you wanted to know the population of London, you could scan the column of city names, starting at the top, until you came to London. Because the cities are listed in alphabetical order, you could also mimic a binary search. You could begin the search near the middle of the column, determine in which half London lies, and recursively apply the binary search to the appropriate half. As you know, a binary search is far more efficient than scanning the entire column of city names from the beginning.

If, however, you wanted to find out which cities in the data collection are in Spain, you would have no choice but to scan the entire data collection. The alphabetical order of the city names does not help you for this problem at all. The data arrangement facilitates the search for a given city, but other types of questions require a complete scan of the data.

The ADT dictionary, or map, or table, also allows you to look up information easily and has a special operation for this purpose. Typically, the items in the ADT dictionary are objects that contain several pieces of data. You can facilitate the retrieval of an item by basing the search on a specified search key. In the dictionary of cities, for example, you could designate City as the search key if you often needed to retrieve information about a city. You can devise implementations of a dictionary that allow the rapid retrieval of the item(s) whose search key matches some specified value. However, if you need to retrieve item(s) based on a value that is not a search key, you will have to inspect the entire dictionary. Therefore, the choice of a search key sends the ADT implementer the following message:

The ADT dictionary uses a search key to identify its items

Arrange the data to facilitate the search for an item, given the value of its search key.

The basic operations that define the ADT dictionary are as follows:

**Note: ADT dictionary operations**

- Test whether a dictionary is empty.
- Get the number of items in a dictionary.
- Insert a new item into a dictionary.
- Remove the item with a given search key from a dictionary.
- Remove all items from a dictionary.
- Get the item with a given search key from a dictionary.
- Test whether a dictionary contains an item with a given search key.
- Traverse the items in a dictionary in sorted search-key order.

For simplicity, we will assume that all items in the dictionary have distinct search keys. This assumption can affect our design in one of several ways:

- Distinct search keys can be a precondition of the insertion operation
- The insertion operation can deny an attempt to insert a new entry whose search key already exists in the dictionary
- The insertion operation can replace an existing entry whose search key matches the search key of a new entry with the new entry

We will choose the first option.

The following operation contract specifies in more detail an ADT dictionary of items with distinct search keys. Figure 18-2 shows a UML diagram for a class of dictionaries.

## ABSTRACT DATA TYPE: DICTIONARY

### DATA

- A finite number of objects, each associated with a search key.

### OPERATIONS

| Pseudocode | Description |
| :--- | :--- |
| isEmpty() | Task: Sees whether this dictionary is empty. Input: None. Output: True if the dictionary is empty; otherwise false. |
| getNumberOfItems() | Task: Gets the number of items in this dictionary. Input: None. Output: The number of items in the dictionary. |
| add(searchKey, newItem) | Task: Inserts an item into this dictionary according to the item's search key. Input: newItem is the data item to be inserted; searchKey is the item's associated search key and differs from all search keys presently in the dictionary. Output: True if the insertion is successful, or false if not. |
| remove(searchKey) | Task: Removes the item with the given search key from this dictionary. Input: searchKey is the search key of the item to be removed. Output: True if the removal is successful, or false if not. |
| clear() | Task: Removes all entries from this dictionary. Input: None. Output: None. |
| getItem(searchKey) | Task: Gets an item with a given search key from this dictionary. Input: searchKey is the search key of the item to be retrieved. Output: The item associated with the given search key. |
| contains(searchKey) | Task: Sees whether this dictionary contains an item with a given search key. Input: searchKey is the search key of the desired item. Output: True if the dictionary contains the designated item, or false if not. |
| traverse(visit) | Task: Traverses this dictionary and calls a given client function once for each item. Input: The client function visit, which exists outside of the ADT implementation. Output: visit's action occurs once for each item in the dictionary and possibly alters the item. |

Various sets of dictionary operations are possible

Our dictionary assumes distinct search keys

You should realize that these operations are only one possible set of dictionary operations. The client may require either a subset of these operations or other operations not listed here to fit the application at hand. It may also be convenient to modify the definitions of some of the operations. For example, these operations assume that no two dictionaries have the same search keys. However, in many applications it is quite reasonable to expect duplicate search keys. If this is the case, you must redefine several of the operations to eliminate the ambiguity that would arise from duplicate search keys. For example, which item should getItem return if several items have the specified search key? You should tailor your definition of the ADT dictionary to the problem at hand.

### FIGURE 18-2 UML diagram for a class of dictionaries

![](img/288a0c22d14d2450c1e772f228f867b0_555_0.png)

Other dictionaries could allow duplicate search keys

Although just the operations add, remove, and getItem in the previous set of operations are sufficient for some applications, you cannot do several significant things without additional operations. For instance, you cannot display all the dictionary items, because you cannot retrieve a data item unless you know the value of its search key. Thus, you cannot display the entire dictionary until you can traverse the dictionary.

traverse visits all dictionary items

The traverse operation visits each item in the dictionary once. In defining this operation, you must specify the order in which the traversal should visit the items. One common specification is to visit the items in sorted order by search key, but perhaps you do not care about the order in which the items are visited. As you will see, the way you define traverse—if you request it at all—can affect the way you implement the dictionary.

> **Note: Search keys**
> 
> The concept of a search key for the dictionary items is essential to the implementation of the dictionary. It is important that the value of the search key remain the same as long as the item is stored in the dictionary. Changing the search key of an existing entry in the dictionary could make that entry or other dictionary entries impossible to find. Thus, the client should not be able to modify the value of an entry's search key once that entry is in the dictionary.

Like the traversal operations for the ADT binary tree, traverse has a visit function as its argument. Because visit can do any number of things—including access the dictionary via the ADT operations—traverse is a versatile operation. We illustrate this versatility with three brief examples, in which the dictionary contains the data for the cities listed in Figure 18-1.

**Examples:** Each of the following tasks will use the city's name as the search key. The class City contains all the information for a city, including its name, country, and population. The class has accessor and mutator methods for each these pieces of data.

### Tasks that use the city's name as the search key

- **Display, in alphabetical order, the name of each city and its population.**

This task requires you to write the city names in alphabetical order. Since the city names are the search keys, traverse must visit items alphabetically by search key. You pass the method the name of the function displayItem, which appears in pseudocode as follows:

```
displayItem(anItem: ItemType): void

    Display anItem.getName()
    Display anItem.getPopulation()
```
