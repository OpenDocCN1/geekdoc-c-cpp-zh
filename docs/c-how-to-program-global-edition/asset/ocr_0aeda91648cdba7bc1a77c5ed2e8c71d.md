```
```cpp
// insert random values between 0 and 14 in the tree
for (unsigned int i = 1; i <= 10; ++i) {
    int item = rand() % 15;
    printf("%3d", item);
    insertNode(&rootPtr, item);
}

// traverse the tree preOrder
puts("\n\nThe preOrder traversal is:");
preOrder(rootPtr);

// traverse the tree inOrder
puts("\n\nThe inOrder traversal is:");
inOrder(rootPtr);

// traverse the tree postOrder
puts("\n\nThe postOrder traversal is:");
postOrder(rootPtr);
}

// insert node into tree
void insertNode(TreeNodePtr *treePtr, int value)
{
    // if tree is empty
    if (*treePtr == NULL) {
        *treePtr = malloc(sizeof(TreeNode));

        // if memory was allocated, then assign data
        if (*treePtr != NULL) {
            (*treePtr)->data = value;
            (*treePtr)->leftPtr = NULL;
            (*treePtr)->rightPtr = NULL;
        } else {
            printf("%d not inserted. No memory available.\n", value);
        }
    }
    else { // tree is not empty
        // data to insert is less than data in current node
        if (value < (*treePtr)->data) {
            insertNode(&((*treePtr)->leftPtr), value);
        }

        // data to insert is greater than data in current node
        else if (value > (*treePtr)->data) {
            insertNode(&((*treePtr)->rightPtr), value);
        }
        else { // duplicate data value ignored
            printf("%s", "dup");
        }
    }
}
```
```

**Fig. 12.19** | Creating and traversing a binary tree. (Part 2 of 3.)