The following are the operations commonly performed on a BST:

+   1. Searching a key
+   2. Inserting a key
+   3. Deleting a key
+   4. Traversing the tree

Program Code 7.10 demonstrates the class for a BST showing the node structure and the function prototypes to operate on.

```
PROGRAM CODE 7.10
class TreeNode
{
    <data type> Key;
    TreeNode *lChild, *rChild;
};

class BSTree
{
    private:
    TreeNode *Root;
    public:
    BSTree() {Root = Null;}       // constructor
    void InsertNode(int Key);
    void DeleteNode(int Key);
    void Search(int Key);
    bool IsEmpty();
};
```

# 7.10.1 Inserting a Node

To insert a new node into a BST, the keys should remain in proper order so that the resulting tree satisfies the definition of a BST.

Let us consider the insertion of the keys Esha, Beena, Deepa, Gilda, Amit, Geeta, and Chetan, into an initially empty tree in the given order as shown in Fig. 7.55.

If the tree is empty, then the first entry, Esha, when inserted, becomes the root, as shown in Fig. 7.55(a). Since Beena is less than Esha, insertion goes into the left subtree of Esha, and so on for all keys. If the tree is not empty, then we must compare the key with the one in the root. Insert() function can be written both recursively as well as non-recursively.