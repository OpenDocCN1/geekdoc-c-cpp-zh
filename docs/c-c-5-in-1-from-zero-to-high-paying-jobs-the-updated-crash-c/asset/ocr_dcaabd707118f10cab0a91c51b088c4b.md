```
value) {
    TreeNode* current = root;
    while (current != nullptr) {
        if (value == current->data
            return true;
        } else if (value < current-
>data) {
            current = current->left;
        } else {
            current = current->right;
        }
    }
    return false;
}

void
BinarySearchTree::inOrderTraversal(Tre
eNode* node) {
    if (node != nullptr) {
        inOrderTraversal(node->left);
        std::cout << node->data << "
";
        inOrderTraversal(node->right);
    }
}

void
BinarySearchTree::preOrderTraversal(Tr
eeNode* node) {
    if (node != nullptr) {
        std::cout << node->data << "
";
        preOrderTraversal(node->left);
        preOrderTraversal(node->
>right);
    }
}

void
BinarySearchTree::postOrderTraversal(T
reeNode* node) {
    if (node != nullptr) {
        postOrderTraversal(node->
>left);
        postOrderTraversal(node->
>right);
        std::cout << node->data << "
";
    }
}
```