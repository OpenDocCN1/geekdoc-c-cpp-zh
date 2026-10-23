# 3.5 Linked Lists

The "list" object in Section 3.4 is implemented as an array of pointers or addresses of objects. This array, however, is too structured: it is not easy to add new items or remove old ones. Furthermore, the number of items is determined once and for all when the list is constructed and cannot be changed afterward. These drawbacks make the "list" data structure unsuitable for many applications. We need to have a more flexible, easily manipulated, and unrestrained kind of list.

![](bbox=[0.32, 0.28, 0.78, 0.58])

Figure 3.2. Schematic representation of a linked list: each item (denoted by a bullet) contains a pointer (denoted by an arrow) to the next item (except the last item, which contains the null (or zero) pointer).

Linked lists don’t use arrays at all. Instead, each item also has a pointer that points to the next item in the list (see Figure 3.2). This structure allows the addition of an unlimited number of items to the linked list if necessary and also allows inserting and dropping items at every location in it.

Accessing items through pointers as above is also called “indirect indexing.” Clearly, it is less efficient than the direct indexing used in arrays, because the items are no longer stored continuously in the computer memory. Nevertheless, its advantages far exceed this disadvantage. Indeed, the freedom to insert and remove items is essential in implementing many useful objects (see Chapter 4). Furthermore, the slight inefficiency in computer resources may be well worth it for the sake of better use of human resources: programmers who use linked lists can benefit from their special recursive structure to implement complex objects, functions, and algorithms.

The linked list is implemented in the template class "linkedList" defined below. (The items in the linked list are of type "T", to be defined later in compilation time.) The "linkedList" class contains two data fields: "item", which contains the first item in the linked list, and "next", which contains the address of the rest of the linked list. Both data fields are declared "protected", so they can be accessed from derived classes later on.

The definition of the "linkedList" object is recursive: the shorter linked list that contains all items but the first one is defined recursively as a "linkedList" object as well and is placed in the address in the field "next". This recursive pattern is useful in many basic operations.