# (FIGURE 10.10 continued)

```
// template <class Item>
// size_t tree_size(const binary_tree_node<Item>* node_ptr)
// Precondition: node_ptr is a pointer to a node in a binary tree (or node_ptr may be
//    NULL to indicate the empty tree).
// Postcondition: The return value is the number of nodes in the tree.
// 
#ifndef BINTREE_H
#define BINTREE_H
#include <cstddef> // Provides NULL and size_t
namespace main_savitch_10
{
    template <class Item>
    class binary_tree_node
    {
    };  || See Figure 10.6 on page 486 for the class definition that goes here.
    
    // NONMEMBER FUNCTIONS for the binary_tree_node<Item>:
    template <class Process, class BTNode>
    void inorder(Process f, BTNode* node_ptr);
    template <class Process, class BTNode>
    void preorder(Process f, BTNode* node_ptr);
    template <class Process, class BTNode>
    void postorder(Process f, BTNode* node_ptr);
    template <class Item, class SizeType>
    void print(const binary_tree_node<Item>* node_ptr, SizeType depth);
    template <class Item>
    void tree_clear(binary_tree_node<Item>*& root_ptr);
    template <class Item>
    binary_tree_node<Item>* tree_copy(const binary_tree_node<Item>* root_ptr);
    template <class Item>
    std::size_t tree_size(const binary_tree_node<Item>* node_ptr);
}
#include "bintree.template" // Include the implementation.
#endif
```