# # ABSTRACT DATA TYPE: DICTIONARY

| Pseudocode | Description |
| :--- | :--- |
| isEmpty() | Task: Sees whether this dictionary is empty.\nInput: None.\nOutput: True if the dictionary is empty; otherwise false. |
| getNumberOfItems() | Task: Gets the number of items in this dictionary.\nInput: None.\nOutput: The number of items in the dictionary. |
| add(searchKey, newItem) | Task: Inserts an item into this dictionary according to the item's search key.\nInput: newItem is the data item to be inserted; searchKey is the item's associated search key and differs from all search keys presently in the dictionary.\nOutput: True if the insertion is successful, or false if not. |
| remove(searchKey) | Task: Removes the item with the given search key from this dictionary.\nInput: searchKey is the search key of the item to be removed.\nOutput: True if the removal is successful, or false if not. |
| clear() | Task: Removes all entries from this dictionary.\nInput: None.\nOutput: None. |
| getItem(searchKey) | Task: Gets an item with a given search key from this dictionary.\nInput: searchKey is the search key of the item to be retrieved.\nOutput: The item associated with the given search key. |
| contains(searchKey) | Task: Sees whether this dictionary contains an item with a given search key.\nInput: searchKey is the search key of the desired item.\nOutput: True if the dictionary contains the designated item, or false if not. |
| traverse(visit) | Task: Traverses this dictionary and calls a given client function once for each item.\nInput: The client function visit, which exists outside of the ADT implementation.\nOutput: visit's action occurs once for each item in the dictionary and possibly alters the item. |

Various sets of dictionary operations are possible

Our dictionary assumes distinct search keys

You should realize that these operations are only one possible set of dictionary operations. The client may require either a subset of these operations or other operations not listed here to fit the application at hand. It may also be convenient to modify the definitions of some of the operations. For example, these operations assume that no two dictionaries have the same search keys. However, in many applications it is quite reasonable to expect duplicate search keys. If this is the case, you must redefine several of the operations to eliminate the ambiguity that would arise from duplicate search keys. For example, which item should getItem return if several items have the specified search key? You should tailor your definition of the ADT dictionary to the problem at hand.