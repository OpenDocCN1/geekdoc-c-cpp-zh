execution time. You learned that linked lists are collections of data items that are “linked up in a chain.” You also saw that an application can perform insertions and deletions at the beginning and end of a linked list. You learned that the stack and queue data structures are constrained versions of lists. For stacks, you saw that insertions and deletions are made only at the top. For queues that represent waiting lines, you saw that insertions are made at the tail and deletions are made from the head. You also learned the binary tree data structure. You saw a binary search tree that facilitated high-speed searching and sorting of data and eliminating duplicate data items efficiently. Throughout the chapter, you learned how to create and package these data structures for reusability and maintainability.

Next, we introduce Java applets—Java programs that typically execute in a browser. We overview the JDK’s sample applets, then show you how to write and execute your own applets. We then introduce the Java Web Start capabilities for launching an applet and installing a desktop shortcut to relaunch the applet in the future without having to revisit the applet’s website.

# Summary

# Section 22.1 Introduction

+   - Dynamic data structures (p. 905) can grow and shrink at execution time.
+   - Linked lists (p. 905) are collections of data items “linked up in a chain”—insertions and deletions can be made anywhere in a linked list.
+   - Stacks (p. 905) are important in compilers and operating systems—insertions and deletions are made only at the top (p. 905) of a stack.
+   - In a queue, insertions are made at the tail (p. 905) and deletions are made from the head (p. 905).
+   - Binary trees (p. 905) facilitate high-speed searching and sorting, eliminating duplicate data items efficiently, representing file-system directories and compiling expressions into machine language.

# Section 22.2 Self-Referential Classes

+   - A self-referential class (p. 905) contains a reference that refers to another object of the same class type. Self-referential objects can be linked together to form dynamic data structures.

# Section 22.3 Dynamic Memory Allocation

+   - The limit for dynamic memory allocation (p. 906) can be as large as the available physical memory in the computer or the available disk space in a virtual-memory system. Often the limits are much smaller, because the computer’s available memory must be shared among many users.
+   - If no memory is available, an OutOfMemoryError is thrown.

# Section 22.4 Linked Lists

+   - A linked list is accessed via a reference to the first node of the list. Each subsequent node is accessed via the link-reference member stored in the previous node.
+   - By convention, the link reference in the last node of a list is set to null to mark the end of the list.
+   - A node can contain data of any type, including objects of other classes.
+   - A linked list is appropriate when the number of data elements to be stored is unpredictable. Linked lists are dynamic, so the length of a list can increase or decrease as necessary.
+   - The size of a “conventional” Java array cannot be altered—it’s fixed at creation time.
+   - List nodes normally are not stored in contiguous memory. Rather, they’re logically contiguous.