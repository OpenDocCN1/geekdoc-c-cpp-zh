To know whether LCHILD and RCHILD fields are referring to the children of the node or to its predecessor and successor, there should be a node structure that clarifies this ambiguity.

# 9.9.1 LINKED REPRESENTATION OF A THREADED BINARY TREE

A linked representation of a threaded binary tree has a node structure as depicted in Figure 9.13.

![](bbox=[0.26, 0.2, 0.73, 0.25])

Figure 9.13 Node structure of a linked representation of a threaded binary tree

This node structure representation includes two additional fields to the linked representation of a binary tree. These two fields act as flags that indicate whether the LCHILD and RCHILD fields represent a thread or a link. If the LEFT THREAD TAG or RIGHT THREAD TAG fields are true then the corresponding LCHILD or RCHILD fields represent threads, else they represent links to the children. The problem dangling threads can also be handled in this representation, because it has a head node to which dangling threads point to. By convention, the head node has its LCHILD pointing to the root node of the threaded binary tree. So the LEFT THREAD TAG is set to false but the RCHILD link points to the head node itself. Figure 9.14(a) shows the linked representation of an empty threaded binary tree and Figure 9.14(b) shows a non-empty threaded binary tree.

![](bbox=[0.3, 0.48, 0.7, 0.53])

(a) Empty threaded binary tree

![](bbox=[0.1, 0.62, 0.9, 0.88])

(b) Non-empty threaded binary tree

Figure 9.14 Linked representation of a threaded binary tree