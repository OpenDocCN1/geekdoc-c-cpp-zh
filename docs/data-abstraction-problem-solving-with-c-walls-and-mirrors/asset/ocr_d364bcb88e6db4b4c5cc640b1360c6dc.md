# SUMMARY

+   1. The ADT list maintains its data by position. Each entry in a list is identified by its position, which is given by an integer, beginning with 1. Thus, the data in a list has an order, but that order is determined by the list's client, not the list itself.
2. You can insert a new entry into a list at a position that ranges from 1 to 1 greater than the current length of the list. Thus, you can insert a new entry before the first entry, after the last entry, or between two current entries.
3. Inserting a new entry into a list renumbers any existing entries that follow the new one in the list.
4. You can remove an entry that is currently at a position that ranges from 1 to the current length of the list. Thus, you can remove the first entry, the last entry, or any interior entry.
5. Removing an entry from a list renumbers any existing entries that follow the deleted one in the list.

# EXERCISES

+   1. Consider an ADT list of integers. Write a pseudocode function that computes the sum of the integers in the list alist. The definition of your function should be independent of the list's implementation.
2. Implement the function swap, as in Checkpoint 3, but remove the assumption that the $i^{th}$ and $j^{th}$ items on the list exist. Return a value that indicates whether the swap was successful.
3. Use the function swap that you wrote in Exercise 2 to write a function that reverses the order of the items in a list alist.
4. Section 8.2 describes the functions displayList and replace. Their definitions are written in terms of the ADT list operations.
   a. What is an advantage and a disadvantage of the way displayList and replace are implemented?
   b. What is an advantage and a disadvantage of defining displayList and replace as operations of the ADT list?
5. Suppose that the ADT list has a method get that returns the position of a given entry within the list. Write specifications for such a method.
6. Write a pseudocode function getPosition at the client level that returns the position of a given entry within a given list.
7. Suppose that the ADT list has a method contains whether the list contains a given entry. Write specifications for such a method.
8. Write a pseudocode function contains at the client level that tests whether a list contains a given entry.
9. The ADT list remove removes from the list the entry at a given position. Suppose that the ADT list has another method remove that removes a given entry from the list. Write specifications for such a method. What does your method do if the list contains duplicate entries?
10. Write a pseudocode function remove at the client level that removes a given entry from a given list.