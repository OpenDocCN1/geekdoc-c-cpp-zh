The ADT sorted list maintains items in sorted order

The ADT sorted list maintains its entries in sorted order. The problem of maintaining sorted data involves more than simply sorting the data. Often you need to insert some new data item into its proper, sorted place. Similarly, you often need to remove some data item. For example, suppose your university maintains an alphabetic list of the students who are currently enrolled. The registrar must add names to and remove names from this list because students constantly enroll in and leave school. These operations should preserve the sorted order of the data.

This chapter specifies the ADT sorted list and then implements it in several ways. A major goal of this chapter is to show you how we can develop a class of sorted lists from an existing class of lists.

# 12.1 Specifying the ADT Sorted List

The ADT list leaves it up to the client to arrange the entries in a given collection. The client can maintain the entries in any order that meets its needs. Recall that to use the insert operation of the ADT list, you must specify both the new entry and its desired position within the list. The ADT sorted list differs from the ADT list in that a sorted list inserts and removes items by their values and not by their positions. For example, the sorted list insertion operation determines the proper position for the new entry according to its value. Since a sorted list is responsible for organizing its entries, it has no operation that inserts a new entry by position. If you were allowed to specify a new entry's position, you might destroy the order of the sorted list's entries.

> Note: The ADT sorted list is a container of items that determines and maintains the order of its entries by their values. For simplicity, we will allow the sorted list to contain duplicate items. Insisting that the sorted list contain only unique items is somewhat more complicated, and we will leave this variation as an exercise.

What other operations do we want for this ADT? We've already mentioned that you can add an entry to the sorted list. Since the sorted list determines the position of a new entry, you could ask the ADT for this position. That is, you could ask for the position of an existing entry or for the position in which a proposed entry would occur if you added it to the list. You could also ask the ADT for the entry at a particular position. And clearly you should be able to remove an entry. We could remove a particular given its value, but we could also remove an entry given its position in the sorted list. We will include both of these removal operations.

Let's itemize the sorted list's operations—including common ones like getting the current number of entries—and specify them more carefully. Note that none of the operations on a sorted list that involve the position of an entry destroys the list's sorted order.

+   **Note: ADT sorted list operations**
+   * Test whether a sorted list is empty.
+   * Get the number of entries in a sorted list.
+   * Insert an entry into a sorted list.
+   * Remove a given entry from a sorted list.
+   * Remove the entry at a given position from a sorted list.
+   * Remove all entries from the sorted list.
+   * Look at (get) the entry at a given position in the list.
+   * Get the position in a sorted list of a given entry.