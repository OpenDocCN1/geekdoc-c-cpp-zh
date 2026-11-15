```
```cpp
int main(){
BinaryTree<int> bt; //Test default constructor
bt.insert(2); //Test insert on empty tree.
bt.insert(10); //Test insert to right subtree.
bt.insert(-2); //Test insert to left subtree.
bt.print(cout); //Test print method.
bt.clear(); // Test clear method.
bt.print(cout);
return 0;
}
```
```

A sample run of the test program produced the following output:

```
-2 2 10
tree is empty
```

The output matches the output of the test of the specific definition.

# Modify!

+   1. Add a public method named printPreOrder(ostream&) and a private recursive method named printPreOrder(ostream&, Node*) that will perform a preOrder print of a tree. The recursive preOrder algorithm is:

```
preOrder traverse:
if(root == null)
return
visit node
preOrder traverse left child
preOrder traverse right child
```

A preOrder print of the tree in Figure 10.8 would result in the output: 14 10 8 22 19 17 27.

+   2. Add a public method named printPostOrder(ostream&) and a private recursive method named printPostOrder(ostream&, Node*) that will perform a postOrder print of a tree. The recursive postOrder algorithm is:

```
postOrder traverse:
if(root == null)
return
postOrder traverse left child
postOrder traverse right child
visit node
```

A postOrder print of the tree in Figure 10.8 would result in the following output: 8 10 17 19 27 22 14.