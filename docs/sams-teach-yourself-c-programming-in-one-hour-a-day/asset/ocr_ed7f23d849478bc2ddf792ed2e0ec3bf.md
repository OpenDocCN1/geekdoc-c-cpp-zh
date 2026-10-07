# LESSON 16 Pointers to Functions and Linked Lists

Lines 30 through 33 add a new link to the start of the list. Line 30 allocates a new data structure. Note that the successful operation of malloc() is assumed—something you would never do in a real program!

Line 31 sets the next pointer in this structure to point to whatever the head pointer contains. Why not simply assign NULL to this pointer? That works if you know the list is empty. If it is written, the code works even if the list already contains some elements. The new first element ends up pointing to the element that was to be first, which is just what you want.

Line 32 makes the head pointer point to the new record, and line 33 stores some data in the record.

Adding an element to the end of the list is a bit more complicated. Although in this case you know the list contains only one element, you cannot assume this in a real program. Therefore, it's necessary to loop through the list, starting with the first element, until you find the last element (as indicated by the next pointer's NULL). Then you will have found the end of the list. This is accomplished on lines 38 through 42. After you have found the last element, it is a simple matter to allocate a new data structure, the old last element point to, and set the new element's next pointer to NULL because it is now the last in the list. This is done on lines 44 through 47. Note that the return type from malloc() is cast to type LINK. (You can learn more about typecasts in Lesson 20, "Exploring the C Function Library.")

The next task is to add an element to the middle of the list—in this case, at the second position. After a new data structure is allocated (line 50), the new element's next pointer is set to point to the element that used to be and is now third in the list (line 51). The first element's next pointer is made to point to the new element (line 52).

Finally, the program prints all records in the linked list. This is a simple matter of starting with the element that the head pointer points to and then processing through the list until the last element is found, as indicated by a NULL pointer. Lines 56 through 61 perform this task.

# Implementing a Linked List

Now that you have seen the ways to add to a list, it's time to see them in action. Listing 16.6 is a rather longer program that uses a linked list to hold a list of five characters. The characters are stored in memory using a linked list. These characters could as easily be given names, addresses, or any other data. To keep the example as simple as possible, only a single character is stored in each link.

What makes this linked list program complicated is the fact that it sorts the links as they are added. Of course, this is also what makes this program valuable. Each link is