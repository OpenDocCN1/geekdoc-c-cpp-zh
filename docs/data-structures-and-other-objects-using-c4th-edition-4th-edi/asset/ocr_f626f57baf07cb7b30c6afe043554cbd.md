There are several parts for you to clarify in your implementation. How do you find the correct value of i in the first step of the pseudocode? (Make sure that your approach uses only the less-than operator to compare items since the Item data type is not required to have other comparison operations.) How do you determine whether the root has children? (Use the private is_leaf member function.)

# Inserting an Item into a B-Tree

The insert member function of the set class adds a new item to the B-tree. It is easier to add a new entry to a B-tree if we relax one of the B-tree rules. In particular, we will allow a somewhat “loose insertion” function to complete its work with the possibility that there is one entry too many in the root node of the B-tree. In other words, a loose insertion might result in MAXIMUM + 1 entries in the root. For example, consider this B-tree where MAXIMUM is 2:

![](bbox=[0.23, 0.4, 0.65, 0.46])

Suppose that we want to add 18 to the tree. The end result of a loose insertion could be the following illegal B-tree:

![](bbox=[0.23, 0.52, 0.65, 0.58])

The B-tree is illegal because the root node has three entries, which is one more than the definition of MAXIMUM. Notice that only the root may have an extra entry after the “loose insertion.” Our plan is for the insert member function to begin by calling another member function that carries out a loose insertion. After the loose insertion, the usual insert member function will examine the root node. If the root node has too many entries, then the insert member function will fix that problem in a way that we’ll describe later. For now, though, we’ll turn our attention to the design of the loose insertion function.

# The Loose Insertion into a B-Tree

From our previous discussion, you can design a specification for a loose insertion. The function will be a private member function called loose_insert. The specification is given here: