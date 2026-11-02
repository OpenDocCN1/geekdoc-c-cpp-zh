```
```cpp
}
}

void RedBlackTree::replace_with(Node* to_be_replaced, Node* replacement)
{
    if (to_be_replaced->parent == nullptr)
    {
        replacement->parent = nullptr;
        root = replacement;
    }
    else if (to_be_replaced == to_be_replaced->parent->left)
    {
        to_be_replaced->parent->set_left_child(replacement);
    }
    else
    {
        to_be_replaced->parent->set_right_child(replacement);
    }
}

void RedBlackTree::fix_after_add(Node* new_node)
{
    if (new_node->parent == nullptr)
    {
        new_node->color = BLACK;
    }
    else
    {
        new_node->color = RED;
        if (new_node->parent->color == RED) { fix_double_red(new_node); }
    }
}

void RedBlackTree::fix_before_remove(Node* to_be_removed)
{
    if (to_be_removed->color == RED) { return; }
    if (to_be_removed->left != nullptr
        || to_be_removed->right != nullptr) // it is not a leaf
    {
        // Color the child black
        if (to_be_removed->left == nullptr)
        {
            to_be_removed->right->color = BLACK;
        }
        else { to_be_removed->left->color = BLACK; }
    }
    else { bubble_up(to_be_removed->parent); }
}

void RedBlackTree::bubble_up(Node* parent)
{
    if (parent == nullptr) { return; }
    parent->color++;
    parent->left->color--;
    parent->right->color--;
    if (bubble_up_fix(parent->left)) { return; }
    if (bubble_up_fix(parent->right)) { return; }
```
```