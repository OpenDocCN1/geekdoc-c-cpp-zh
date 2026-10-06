Chapter 11

Menu-Driven Programs

# Checkpoint

11.4 Explain why most menu-driven programs use a loop to redisplay the menu after the user's selected action has been performed.

11.5 If a program uses a loop to display a menu repeatedly, how does the user end the program?

# 11.4 Multiple-Level Menus

CONCEPT: A multiple-level menu has a main menu and one or more submenus.

The programs that you have seen in this chapter are simple enough that all of their menus fit nicely in a single menu. When the user selects an option from the menu, the program immediately performs that operation and then redisplays the menu (or the program ends it does not use a loop to redisplay the menu). This type of menu system is called a single-level menu.

Often, programs are more complex and one menu isn't sufficient. For example, suppose you are designing a program that a business can use to perform the following operations:

+   1. Process a sale
2. Process a return
3. Add a record to the inventory file
4. Search for a record in the inventory file
5. Modify a record in the inventory file
6. Delete a record in the inventory file
7. Print an inventory list report
8. Print a list of inventory items by cost
9. Print a list of inventory items by age
10. Print a list of inventory items by retail value

Because there are so many items in this list, you probably wouldn't display them all in one menu. Users often have trouble sorting the items in a menu when given too many choices.

A better approach is to use a multiple-level menu. A program that uses a multiple-level menu displays when the program starts, showing only a few items, and then displays submenus when the user makes a selection. For example, the main menu appears as follows:

Main Menu

+   1. Process a Sale or a Return
2. Update the Inventory File
3. Print an Inventory Report
4. Exit the Program

![](bbox=[0.1415, 0.2235, 0.2115, 0.2635])

![](bbox=[0.1865, 0.0835, 0.2215, 0.1135])