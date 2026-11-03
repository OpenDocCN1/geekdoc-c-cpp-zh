# Chapter 8: Binary Trees

A tree is a finite set of elements, often known as nodes. Every tree has a unique starting node, called the root node, whereas the remaining nodes are a disjoint collection of subtrees of this root node. Each node keeps track of its parents or/and children so that traversal can be made possible. A node with no children is called a leaf node or a terminal node.

A binary tree is a tree whose nodes can have a maximum of two children. A binary tree is a data structure which comprises of two possible sub-elements of every node, called left child and right child. If a node does not have a left or right child, they are assigned NULL values. Each link must point at a new object not pointed at or be NULL.

The general form a node in a binary tree is as follows:

```
struct node
{
Char value;
Node *left, *right ;
}
```