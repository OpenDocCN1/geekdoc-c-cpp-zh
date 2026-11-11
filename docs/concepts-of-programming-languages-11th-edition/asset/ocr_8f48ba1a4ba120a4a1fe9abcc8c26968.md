are not types in the sense that imperative languages have types. In fact, the original Lisp was a typeless language. Atoms are either symbols, in the form of identifiers, or numeric literals.

Recall from Chapter 2, that Lisp originally used lists as its data structure because they were thought to be an essential part of list processing. As it eventually developed, however, Lisp rarely requires the general list operations of insertion and deletion at positions other than the beginning of a list.

Lists are specified in Lisp by delimiting their elements with parentheses. The elements of **simple lists** are restricted to atoms, as in

```
```lisp
(A B C D)
```
```

Nested list structures are also specified by parentheses. For example, the list

```
```lisp
(A (B C) D (E (F G)))
```
```

is a list of four elements. The first is the atom *A*; the second is the sublist `(B C)`; the third is the atom *D*; the fourth is the sublist `(E (F G))`, which has as its second element the sublist `(F G)`.

In a Lisp implementation, a list is usually stored as linked list structure in which each node has two pointers, one to reference the data of the node and the other to form the linked list. A list is referenced by a pointer to its first element. The internal representations of our two example lists are shown in Figure 15.1. Note that the elements of a list are shown horizontally. The last

![](bbox=[0.03, 0.642, 0.95, 0.956])