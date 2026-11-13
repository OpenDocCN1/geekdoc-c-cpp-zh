```
{
 if(parent->Lchild == temp)
 parent->Rchild = Null;
 else
 parent->Rchild = Null;
 }
 else
 root = Null;
 delete temp;
 return(root);
 }
 else if(temp->Lchild!=Null&&temp->Rchild ==
 Null)
 //case of BST node having left children
 {
 //cout << "\n only left";
 if(temp! = root)
 {
 if(parent->Lchild == temp)
 parent->Lchild = temp->Lchild;
 else
 parent->Rchild = temp->Lchild;
 }
 else
 root = temp->Lchild;
 delete temp;
 return(root);
 }
 }
}
```

# 7.10.4 Binary Tree and Binary Search Tree

We have studied both binary tree and BST. A BST is a special case of the binary tree. The comparison of both yields the following points:

+   1. Both of them are trees with degree two, that is, each node has utmost two children. This makes the implementation of both easy.
+   
+   2. The BST is a binary tree with the property that the value in a node is greater than any value in a node's left subtree and less than any value in a node's right subtree.