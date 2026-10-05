As we can see, the public version of the function calls its private version and passes the root pointer to it. Let us look at the private function of the function.

```
/*
  Private function to pre-order traversal. Will be called from the public function.
*/
void BST::preorder(BSTNode * nodePtr)
{
  /*
    As long as the passed pointer is not NULL ...
  */
  if(nodePtr != NULL) {
    /*
      display the value of the current node first
    */
    cout << nodePtr -> val() << endl;
    /*
      then call the function recursively for the left child
    */
    preorder(nodePtr -> getLeft());
    /*
      and call the function recursively for the right child.
    */
    preorder(nodePtr -> getRight());
  }
}
```

This function is actually very simple. When this is called for the first time, the value of root gets copied to nodePtr. If nodePtr is NULL, then the function terminates without doing anything. Otherwise, it displays the value of the first node. It traverses the left sub-tree by passing the value of the left pointer of the node, where nodePtr points to the recursive call to the function. Thereafter, it traverses the left-right sub-tree by passing the value of the right pointer of the node where nodePtr points to the recursive call to the function. Keep in mind that as the first recursive call to the function is executing, the second recursive call will not start. Also, in every new generation of the function, nodePtr will point at the root node of the lower sub-tree.
inorder() and postorder() functions can be explained in the same way.

# Summary

Data structures are special in ways in which data are arranged and related to each other during runtime. Each piece of data is embedded in a node that contains the piece of data itself along with one or more pointers that either point at other similar nodes or have null values.

Linked lists are data structures. They consist of nodes that are linked to each other in a linear fashion. Each node in a single linked list is an object made up of two parts. The first part is the data carried by the node. The second part of each node is a pointer