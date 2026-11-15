The list and list iterator objects are created and handled directly from the C source code. The `list` ACD datatype is not for generic lists; it is used to handle selections from a menu.

# ## 6.16.2 AJAX library files

AJAX library files for handling lists are listed in the table below. Library file documentation, including a complete description of datatypes and functions, is available at:

`http://emboss.open-bio.org/rel/dev/libs/`

| Library file documentation | Description |
| --- | --- |
| ajlist | General list handling |

`ajlist.h/c`. All the functions you are likely to ever need for the creation and control of linked lists. They define the basic list object (`AjPList`) which includes the list node object (`AjPListNode`) as a nested substructure, and a list iteration object (`AjIList`). It also includes static data structures and functions for handling lists at a low level. You are unlikely to need the low-level code unless you plan to implement code to extend the core functionality of the library.

# ## 6.16.3 ACD datatypes

There is no dedicated ACD datatype for handling general lists, the `list` ACD datatype being used to handle selections from a menu (see Section 6.19, ‘Handling menus’). For numeric arrays the `array` datatype can be used (see Section 6.17, ‘Handling arrays’).

# ## 6.16.4 AJAX datatypes for handling lists

There are three AJAX datatypes for handling lists:

+   - `AjPList`: Basic linked list
+   - `AjPListNode`: Node in a linked list, included as a nested substructure in `AjPList`
+   - `AjIList`: Used for list iteration.

# ## 6.16.5 Types of list

The functions handle lists of nodes which include a pointer variable to the node data. The generic list handling functions have `void *` parameters which must be cast to the correct type when an argument is passed. For convenience, a dedicated set of functions for handling string lists are provided that are cast to the appropriate type. Such functions all have the prefix `ajListstr` to distinguish them from the general functions (which have the prefix `ajList`).