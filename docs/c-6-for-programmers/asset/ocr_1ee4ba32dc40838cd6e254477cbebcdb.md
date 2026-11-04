# ### Adding and Inserting Elements

The `Add` and `Insert` methods add elements to the `List` (lines 17–18):

+   - The `Add` method *appends* its argument to the end of the `List`.
+   - The `Insert` method inserts a new element at the specified position.

Insert’s first argument is an index—as with arrays, collection indices start at zero. The second argument is the value to insert at the specified index. To make room for the new element, the indices of the elements at the specified index and above each increase by one—in this case, "red" initially was at index 0, but now is at index 1, so that "yellow" can be inserted at index 0.

# ### Count and Capacity

Lines 21–22 display the `List`’s `Count` (2) and `Capacity` (4) after the `Add` and `Insert` operations. When line 17 executes, the `List` grows, increasing its `Capacity` to 4 so that the `List` can accommodate *four elements*. One of these elements is immediately occupied by "red". At this point, the `List`’s `Count` is 1. When line 18 executes, there’s still room for three more elements, so "yellow" is inserted and the `Count` becomes 2.

# ### Iterating Through a List’s Contents

Lines 27–30 display the items in the `List`. Like array elements, `List` elements can be accessed by placing the index in square brackets after the `List` variable’s name. The indexed `List` expression can be used to modify the element at the index. Lines 34–37 display the `List` using the preferred `foreach` statement.

# ### Adding More Elements and Growing the List

Lines 39–51 add more elements to the `List`, then display its `Count`, `Capacity` and contents once again.

# ### Removing Elements

The `Remove` method deletes the first element with a specific value (line 53), returning `true` if successful and `false` otherwise. Lines 57–60 show the `List`’s contents after line 53 executes. A similar method, `RemoveAt`, removes the element at the specified index (line 62). When an element is removed through either of these methods, the indices of all elements above that index decrease by one—the opposite of the `Insert` method. Lines 66–69 show the `List`’s contents after line 62 executes. Lines 72–73 display the `List`’s `Count` (2) and `Capacity` (4) after the remove operations. At this point, there’s room in the `List` for two more elements.

# ### Determining Whether an Element Is in the List

Line 77 uses the `Contains` method to check whether an item is in the `List`. The `Contains` method returns `true` if the element is found in the `List` and `false` otherwise. The method compares its argument to each element of the `List` in order until the item is found, so using `Contains` on a large `List` is inefficient.

# ### Adding More Elements and Growing the List

Lines 79–81 add three more elements to the `List`. Before lines 79–80 execute, `Count` is 2 and `Capacity` is 4, so there’s room in the `List` for the two new elements added by those