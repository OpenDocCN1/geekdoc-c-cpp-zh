WARNING
Do not use typedef to define a new structure variable when creating a linked list. I'm not using typedef in Listing 20-7, so it's not an issue with the code, but many C programmers use typedef with structures. Be careful!

WARNING
The third traditional linked-list variable is named new. I use next instead because new is a reserved word in C++. Though you can use new in your C code, it's best not to confuse the two. Therefore, I've rewritten the code to use the next variable name, which is also part of the linked-list structure shown in Listing 20-7.

At Line 17, the first pointer is allocated. This pointer forms the base address of the linked list, and it must never be altered or else the entire list is lost. Therefore, at Line 24, it's assigned to the current pointer, which is used to assign values in the current list structure.

At Line 32, the next member of the current structure is allocated to a new stk structure in memory. (The line is split so that it doesn't mess up this book's layout.) Upon success, at Line 40 the current structure pointer is assigned to current->next, and this new structure's data is filled.

The linked list is capped at Line 45. The NULL pointer is assigned to the last structure's next member.

Line 50 resets the list to the base, assigning pointer current to first. A while loop outputs the list as long as the current pointer isn't NULL. This pointer is updated at Line 58.

# Exercise 20-11: Type the source code from Listing 20-7 into your editor, or just copy over the source code from Exercise 20-10 and modify it. Even though it's long, type it in because you need to edit it again later (if you're not used to that by now). Build and run.

Figure 20-1 illustrates the concept of the linked list based on what Listing 20-7 does.

# FIGURE 20-1:
A linked list in memory.

![](bbox=[0.28, 0.75, 0.92, 0.9])

Unlike arrays, structures in a linked list aren't numbered. Instead, each structure is linked to the next one in the list. Providing that you know the address of the first structure, you can work through the list until the end, which is marked by a NULL pointer.