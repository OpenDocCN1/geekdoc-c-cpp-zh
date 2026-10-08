# Chapter 19 Custom Linked Data Structures

```
56 // perform postorder traversal of tree
57 Console.WriteLine($"\nnPostorder traversal of {treeType}");
58 tree.PostorderTraversal();
59 }
60 }
```

Inserting into intTree:
8 2 4 3 1 7 5 6

Preorder traversal of intTree
8 2 1 4 3 7 5 6

Inorder traversal of intTree
1 2 3 4 5 6 7 8

Postorder traversal of intTree
1 3 6 5 7 4 2 8

Inserting into doubleTree:
8.8 2.2 4.4 3.3 1.1 7.7 5.5 6.6

Preorder traversal of doubleTree
8.8 2.2 1.1 4.4 3.3 7.7 5.5 6.6

Inorder traversal of doubleTree
1.1 2.2 3.3 4.4 5.5 6.6 7.7 8.8

Postorder traversal of doubleTree
1.1 3.3 6.6 5.5 7.7 4.4 2.2 8.8

Inserting into stringTree:
eight two four three one seven five six

Preorder traversal of stringTree
eight two four three one five seven six

Inorder traversal of stringTree
eight five four one seven six three two

Postorder traversal of stringTree
six five seven one three four two eight six

**Fig. 19.24** | Testing class with IComparable objects. (Part 3 of 3.)

Method PopulateTree (33–44) receives arguments as an Array containing the initializer values for the Tree, a Tree in which the array elements will be placed and a string representing the Tree name, then inserts each Array element into the Tree. Method TraverseTree (46–59) receives arguments as an Array and a string representing the Tree name, then outputs the preorder, inorder and postorder traversals of the Tree. The inorder traversal of each Tree outputs the data in *sorted order* regardless of the data type stored in the Tree. Our polymorphic implementation of class Tree invokes the appropriate data type's CompareTo method to determine the path to each value point using the standard binary-search-tree insertion rules. Also, notice that the Tree of strings appears in alphabetical order.