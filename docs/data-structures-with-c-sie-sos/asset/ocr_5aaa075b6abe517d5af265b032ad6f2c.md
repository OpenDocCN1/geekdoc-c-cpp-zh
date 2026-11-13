of pointers giving the positions of his or her customers, as in Fig. 1.6. The main disadvantage of this representation is that each salesperson may have many pointers and the set of pointers will change as customers are added and deleted.

| Salesperson | Pointer |
|---|---|
| Jones | 3, 6 |
| Ray | 2, 4, 7, 9 |
| Smith | 1, 5, 8 |

Fig. 1.6

Another very popular way to store the type of data in Fig. 1.4 is shown in Fig. 1.7. Here each salesperson has one pointer which points to his or her first customer, whose pointer in turn points to the second customer, and so on, with the salesperson’s last customer indicated by a 0. This is pictured with arrows in Fig. 1.7 for the salesperson Ray. Using this representation one can easily obtain the entire list of customers for a given salesperson and, as we will see in Chapter 5, one can easily insert and delete customers.

The representation of the data in Fig. 1.7 is an example of linked lists. Although the terms “pointer” and “link” are usually used synonymously, we will try to use the term “pointer” when an element in one list points to an element in a different list, and to reserve the term “link” for the case when an element in a list points to an element in that same list.

| Customer | Link |
|---|---|
| Adams | 5 |
| Brown | 4 |
| Clark | 6 |
| Drew | 7 |
| Evans | 8 |
| Farmer | 0 |
| Geller | 9 |
| Hill | 0 |
| Infeld | 0 |

| Salesperson | Pointer |
|---|---|
| Jones | 3 |
| Ray | 2 |
| Smith | 1 |

Fig. 1.7

# Trees

Data frequently contain a hierarchical relationship between various elements. The data structure which reflects this relationship is called a _rooted tree graph_ or, simply, a _tree_. Trees will be defined and discussed in detail in Chapter 7. Here we indicate some of their basic properties by means of two examples.

# Example 1.4 Record Structure

Although a file may be maintained by means of one or more arrays, a record, where one indicates both the group items and the elementary items, can best be described by means of a tree structure. For example, an employee personnel record may contain the following data items:

Social Security Number, Name, Address, Age, Salary, Dependents

However, Name may be a group item with the subitems Last, First and MI (middle initial). Also, Address may be a group item with the subitems Street address and Area address, where Area itself may be a group item having subitems City, State and ZIP code number. This hierarchical structure is pictured in Fig. 1.8(a). Another way of picturing such a tree structure is in terms of levels, as in Fig. 1.8(b).