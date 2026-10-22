4.6 Add to the LList class implementation a member function to reverse the order of the elements on the list. Your algorithm should run in Θ(n) time for a list of n elements.

4.7 Write a function to merge two linked lists. The input lists have their elements in sorted order, from lowest to highest. The output list should also be sorted from lowest to highest. Your algorithm should run in linear time on the length of the output list.

4.8 A circular linked list is one in which the next field for the last link node of the list points to the first link node of the list. This can be useful when you wish to have a relative positioning for elements, but no concept of an absolute first or last position.

+   (a) Modify the code of Figure 4.8 to implement circular singly linked lists.
+   (b) Modify the code of Figure 4.14 to implement circular doubly linked lists.

4.9 Section 4.1.3 states “the space required by the array-based list implementation is Ω(n), but can be greater.” Explain why this is so.

4.10 Section 4.1.3 presents an equation for determining the break-even point for the space requirements of two implementations of lists. The variables are D, E, P, and n. What are the dimensional units for each variable? Show that both sides of the equation balance in terms of their dimensional units.

4.11 Use the space equation of Section 4.1.3 to determine the break-even point for an array-based list and linked list implementation for lists when the sizes for the data field, a pointer, and the array-based list’s array are as specified.

+   (a) The data field is eight bytes, a pointer is four bytes, and the array holds twenty elements.
+   (b) The data field is two bytes, a pointer is four bytes, and the array holds thirty elements.
+   (c) The data field is one byte, a pointer is four bytes, and the array holds thirty elements.
+   (d) The data field is 32 bytes, a pointer is four bytes, and the array holds forty elements.

4.12 Determine the size of an int variable, a double variable, and a pointer on your computer. (The C++ operator sizeof might be useful here if you do not already know the answer.)

+   (a) Calculate the break-even point, as a function of n, beyond which the array-based list is more space efficient than the linked list for lists whose elements are of type int.
+   (b) Calculate the break-even point, as a function of n, beyond which the array-based list is more space efficient than the linked list for lists whose elements are of type double.