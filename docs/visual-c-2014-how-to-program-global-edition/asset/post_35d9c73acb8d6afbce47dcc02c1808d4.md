
# 704 Chapter 15 Graphical User Interfaces with Windows Forms: Part 2

Process class System.Diagnostics namespace
root node TabControl class
SelectedIndex property of class ComboBox Page class
SelectedIndex property of class ListBox Pages property of class TabControl
Changed event of class ListBox Text property of class TabPage
Changed event of class ListBox Tick event of class Timer
Indices property of class ComboBox titled window
SelectedItem property of class ListBox TimeOfDay property of class DateTime
SelectedItem property of class ListBox Class
Items property of class ListBox Long method of class DateTime
SelectionMode enumeration LongTime method of class DateTime
SelectionMode property of ListBox ToolStripMenuItem

separator bar trec
ShortcutKeyDisplayString property of class TreeNode
Shortcuts property of class TreeNodeCollection type
ToolTip MenuItem View class
ShowShortcuts property of class Tree EventArgs
ToolTip MenuItem Usercontrol Value property of class DateTime
sibling node Changed event of class DateTimePicker
single document interface (SDI) verbatim string
SmallImageList property of class ListView View property of class ListView
Start method of class Process visual inheritance

## Self-Review Exercises

- 15.1 State whether each of the following is true or false. If false, explain why.
  a) Menus provide groups of related classes.
  b) Menu items can display ComboBoxes, checkmarks and access shortcuts.
  c) The ListControl allows only one selection (like a RadioButton).
  d) A ComboBox control typically has a drop-down list.
  e) Deleting a node in a TreeView deletes its child nodes.
  f) The user can select only one item in a ListControl.
  g) A TabPage can act as a container for RadioButtons.
  h) An MDI window can have MDI children.
  i) MDI windows can be moved outside the boundaries of their parent window.
  j) There are two basic ways to create a customized control.

- 15.2 Fill in the blanks of each of the following statements:
  a) Method of class Process can open files and web pages, similar to the Runcommand in Windows.
  b) If more elements appear in a ComboBox than can fit, a(n) appears.
  c) The top-level node in a TreeView is the node.
  d) A(n) and a(n) can display icons contained in an ImageControl.
  e) The property allows a menu to display a list of active child windows.
  f) Class allows you to combine controls into a single custom control.
  g) The saves space by layering TabPages on top of each other.
  h) The window layout option allows all MDI windows the same size and layers so every item is visible (possible).
  i) are typically used to display hyperlinks to other resources, files or web pages.

## Answers to Self-Review Exercises

15.1 a) False. Menu provides groups of related commands, b) True c) False. It can have single or multiple selection. d) True e) True f) False. The user can select one or more items. g) True h) False. Only an MDI parent window can have MDI children. MDI parent cannot have an MDI child. i) False. MDI children cannot move outside their parent window. j) False. There are three ways: 1) Derive from an existing control, 2) use a UserControl or 3) derive from Control and create a control from scratch.

15.2 a) Start. b) scrollbar. c) root. d) listView, TreeView. e) MWindowListItem. f) UserController. g) TabControl. h) Cascade. i) LinkLabels.

## Exercises

15.3 (Adding and Removing from ComboBox) Write an app that displays décor products in a ComboBox. A text box and a button are used to add items to ComboBox. Selecting an item in the ComboBox, it gets removed from the ComboBox. Display the count of items.

15.4 (Adding items in ListBox) Modify your solution to the previous exercise by adding a ListBox to. When the user selects an item from the ComboBox, remove the item from the ComboBox and add it to List. The program should ensure that the ComboBox contains at least one item. If it does not display, use a message box, then terminate the program execution when the user dismisses the message box.

15.5 (Sorting Strings) Write an app that allows the user to enter strings in a TextBox. String input is added to List. As each string is added to List, ensure that the strings are sorted in order. [Note: Use Sort property].

15.6 (File Browser) Create a file browser (similar to Windows Explorer) based on the programs in Figs. 15.14, 15.28 and 15.31. The file browser should have a TreeView, which allows the user to browse directories. There should also be a ListView, which displays the contents (all subdirectories and files) of the directory being browsed. Double clicking a file in the ListView should open it, and double clicking an entry in either ListView or the ListView should show it. If a file or directory is denied because of its permissions, show the error.

15.7 (MDI Text Editor) Create an MDI text editor. Each window should contain a RichTextBox. The MDI parent should have a Format menu, with submenus to control the size, font and color of the text in the active child window. Each submenu should have at least three options. In addition, the parent should have a New items (create a new child), Close (close the active child) and Exit (the app). The parent should have a Window menu to display a list of the child windows and their layouts.

15.8 (Login Control) Create an MDI app with child windows that each have a Panel for drawing. Add menus to the MDI app that allow the user to modify the size and color of the paintbrush. When running this app, be aware that if one of the windows overlaps another, the Panel will be cleared.

15.9 (Restaurant Calculator) Create a restaurant app that calculates a bill. The app should display all the items from Fig. 15.52 in ComboBoxes. Each ComboBox should contain a category of food (Beverage, Appetizer, Main and Dessert). Each item selected in the ComboBox adds the price of that item to the bill. The user can click the Clear Button to reset the Subtotal, Tax and Total.

# 15 Graphical User Interfaces with Windows Forms: Part 2

| Name | Category | Price | Name | Category | Price |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Soda | Beverage | $1.95 | Chicken Alfredo | Main Course | $13.95 |
| Tea | Beverage | $1.50 | Chicken Picatta | Main Course | $13.95 |
| Coffee | Beverage | $1.25 | Turkey Club | Main Course | $11.95 |
| Mineral Water | Beverage | $2.95 | Lobster Pie | Main Course | $19.95 |
| Juice | Beverage | $2.50 | Prime Rib | Main Course | $20.95 |
| Milk | Beverage | $1.50 | Shrimp Scampi | Main Course | $18.95 |
| Buffalo Wings | Appetizer | $5.95 | Turkey Dinner | Main Course | $13.95 |
| Buffalo Fingers | Appetizer | $6.95 | Stuffed Chicken | Main Course | $14.95 |
| Potato Skins | Appetizer | $8.95 | Apple Pie | Dessert | $5.95 |
| Nachos | Appetizer | $8.95 | Sunday | Dessert | $3.95 |
| Mushroom Caps | Appetizer | $10.95 | Carrot Cake | Dessert | $5.95 |
| Shrimp Cocktail | Appetizer | $12.95 | Mud Pie | Dessert | $4.95 |
| Chips and Salsa | Appetizer | $6.95 | Apple Crisp | Dessert | $5.95 |
| Seafood Alfredo | Main Course | $15.95 | | |

**Fig. 15.52** Food items and prices.

15.10 (Using TabPages) Create an app that contains three TabPages. On the first TabPage, place a checkbox with six items. On the second TabPage, place six TextBoxes. On the last TabPage, place six LinkLabels. The user's selections on the first TabPage should specify which of the six LinkLabels will be displayed. To hide or display a LinkLabel's value, use its Visibl property. Use the second TabPage to modify the web page that is opened by the LinkLabels.

# 16

# # Strings and Characters: A Deeper Look

# Objectives

In this chapter you'll:

- Create and manipulate immutable character-string objects of class string and mutable character-string objects of class StringBuilder.
- Use various methods of classes string and StringBuilder.
- Manipulate character objects of struct Char.
- Use regular-expression classes Regex and Match.

![](img/57baed2319be0bb1b5f98674846f2711_707_0.png)
