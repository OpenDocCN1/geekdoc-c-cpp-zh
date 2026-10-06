# 226 Plug-In JavaScript: 100 Power Solutions

FIGURE 8-5
Creating a folding menu side bar.

![](bbox=[0.298, 0.108, 0.836, 0.352])

About the Plug-In
The plug-in requires a pair of arrays of heading and contents and then displays a folding menu based on the styles and actions you supply. It takes the following arguments:

+   * **headings** An array of objects and/or object IDs
* **contents** An array of objects and/or object IDs
* **action** The menu action type, either 'hover' or 'click'
* **type** The type of transitions to use, out of contents 'fade', 'inflate', 'zoom', or 'instant'
* **multi** If true or 1, more than one section can be open at a time
* **w, h** If type is 'inflate' or 'zoom', these arguments specify the width, height, or dimensions be modified during transitions
* **mssec1** The transition in milliseconds of popping down
* **mssec2** The transition in milliseconds of popping up
* **interruptible** If true or 1, the PopUp() and PopDown() plug-in is interrupted by another on the same id

# Variables, Arrays, and Functions

| j | Local variable for iterating through the headings array |
| PO_C | Property of each heading containing the object in the contents array to which it refers |
| PO_IsUp | Property of each object in the contents array, which is false when an object is popped down, otherwise the object is popped up |
| cursor | Property of each heading's style object used for changing the mouse pointer when over the heading |