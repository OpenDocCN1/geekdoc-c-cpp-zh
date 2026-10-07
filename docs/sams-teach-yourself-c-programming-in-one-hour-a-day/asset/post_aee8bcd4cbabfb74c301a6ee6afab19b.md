
# Understanding Linked Lists

413

If this link isn't the first, the function continues until the else at line 87. Line 90 checks to whether the new link goes at the beginning of the list. As you should remember, this is one of the three cases for adding a link. If the link does go first, line 92 sets the next_rec pointer in the new link to point to the previous "first" link. Line 93 then sets the head pointer, first, to point to the new link. This results in the new link being added to the beginning of the list.

If the new link isn't the first to be added to an empty list, and if it's added at the first position in an existing list, you know it must be in the middle or at the end of the list. Line 97 and 98 set the tmp_rec and prev_rec pointers that were declared earlier. The pointer tmp_rec is set to the address of the second link in the list, and prev_rec is set to the first link in the list.

You should note that if there is only one link in the list, the tmp_rec will be equal to NULL. This is because tmp_ptr is set to the next_ptr in the first link, which will be equal to NULL Line 102 checks for this special case. If tmp_rec is NULL you know that this is the second link being added to the list. Because you know the new link doesn't come before the first link, it can go only at the end. To accomplish this, you simply set prev_rec->next_ptr to the new link, and then you're done.

If the tmp_rec pointer isn't NULL, you know that you already have more than two links in your list. The statement on lines 110 through 129 loops the rest of the links to determine where the new link's data should be placed. Line 112 checks whether the new link's data is less than the link currently being pointed to. If it is, this is where you want to add the link. If the new link is greater than the current link's data, you need to look at the next link in the list. Lines 126 and 127 set the pointers tmp_rec and next_rec to the next link.

If the character is "less" than the current link's character, you would follow the logic presented earlier this lesson for adding to the middle of a linked list. This process can be seen in lines 114 through 122. Line 114, the new link's pointer is set to equal the current link's address (tmp_rec). Line 121 sets the previous link's next pointer to point to the new link. After this, you're done. The code uses a break statement to get out of the while loop.

| NOTE |
|---|
| Lines 115 through 120 contain debugging code that is the listing for you to see. These lines could be removed; however, as long as the program is running correctly, they will never be called. After the new link's pointer is set to the current pointer, it should be equal to the previous link's next pointer, which also points to the current record. If they aren't equal, something went wrong |

# LESSON 16 Pointers to Functions and Linked Lists

The previously covered logic takes care of links being added to the middle of the list. If the end of the list is reached, the while loop in on lines 110 through 129 ends without adding the link. Lines 132 through 144 take care of adding the link to the end.

If the last link in the list was reached, tmp_rec->next_rec equals NULL. Line 132 checks for this condition. Line 134 checks to see whether the link goes before or after the last link. If it goes after the last link, the last link's next_rec is set to the new link (line 132), and the new link's pointer is set to NULL (line 142).

# Improving Listing 16.6

Linked lists are not the easiest to learn. As you can see from Listing 16.6, however, they are an excellent way of storing data in a sorted order. Because it's easy to add data items anywhere in a linked list, the care of keeping a list of data items in sorted order with a linked list is a lot simpler than it would be if you used, say, an array. This linked list could be converted to sorted names, phone numbers, or any other data. In addition, although this there sorted in ascending order (A to Z), it just as easily have sorted in descending order (Z to A).

# Deleting from a Linked List

The capability to add information to a linked list is essential, but there will be times when you will want to remove information, too. Deleting links, or elements, is similar to adding them. You can delete links from the beginning, middle, or end of linked lists. In each case, the appropriate pointers need to be adjusted. Also, the memory used by the deleted link needs to be freed.

> Don't forget to free memory when deleting links!

| DO | DON'T |
|---|---|
| DO understand the difference between calloc() and malloc(). Most important, remember that malloc() doesn't initialize allocated memory—calloc() does. | DON'T forget to free any memory allocated for links when deleting them. |

# Summary

This lesson further your knowledge and experience with pointers. You learned to declare and use pointers to functions, an important and flexible programming tool. Finally, you learned how to implement linked lists, a powerful and flexible data storage method.

The last two lessons have covered complicated topics, they're exciting as well. With your new knowledge of pointers, you're really getting into some of the sophisticated capabilities of the C language. Power and flexibility are among the main reasons C is such a popular language.

# Q&A

- Is it necessary to use the concepts presented in this lesson to take advantage of C?
- You can use C without ever any advanced pointer concepts; however, you won't take advantage of the power that C offers. Pointer manipulations such as those shown in this lesson can make many programming tasks easier and more efficient.

- Are there other times when function pointers are useful?
- Yes. Pointers to functions are also used with menus. Based on a value returned from a menu, a pointer is set to the function that should be called based on the menu choice.

- Name two major advantages of linked lists.
- The size of a linked list can be increased or decreased while the program is running; it doesn't have to be predefined when you write the code. Two: It's easy to keep a list in sorted order because elements can be easily added or deleted.

# Workshop

The Workshop provides quiz questions to help you solidify your understanding of the material and exercises to provide you with experience using what you've learned.

# Quiz

- 1. What is a pointer to a function?
- 2. Write a declaration of a pointer to a function that returns type char and takes an array of pointers to char as an argument.
- 3. You might have answered 2 with char *ptr(x[]); What is wrong with this declaration?
- 4. When defining a data structure to be used in a list, what is the one element that must be included?
- 5. What does it mean if the head pointer is equal to NULL?
- 6. How are single-linked lists connected?
- 7. What to the following declare?
  a. char *z[10];
  b. char *y(int field);
  c. char (*x)(int field);

# Exercises

- 1. Write a declaration for a pointer to a function that takes an integer as an argument and returns type float variable.
- 2. Write a declaration for an array of pointers to functions. The functions should all take a character string as a parameter and return an integer. What could such an array be used for?
- 3. Write a structure that is to be used in a single-linked list. This structure should hold your friends' names and addresses.

> Because of the many possible solutions, answers are not provided for the following exercises.

- 4. ON YOUR OWN: Write a program that uses pointers to double variables to accept 10 numbers from the user, sort them, and print them to the screen. (Hint: See Listing 16.3.)
- 5. ON YOUR OWN: Modify the program in the previous exercise to allow the user to specify whether the sort order is ascending or descending.

# # LESSON 17
# Using Disk Files

Most of the programs you write use files written to a hard drive. These files contain information that serves one purpose or another: data storage, configuration information, and so on. In this lesson you learn

- How to relate streams to disk files
- About C’s two disk file types
- The commands for opening a file
- How to write data to a file
- Reading data from a file
- Disk file management
- Using temporary files
