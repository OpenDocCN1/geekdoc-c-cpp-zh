structure of a tree that stores its data at its nodes. The tree should be the interface for the user, while a node should essentially serve only as a data holder.

unique_ptr<Node> is a container for a Node and is explained in detail in Chapter 20. Because the Tree should hold arbitrary data, I wrote Tree and Node as class templates. So you will be able to write Tree<int>, similar to vector<int>. You will learn exactly how this works in Chapter 23.

```
// https://godbolt.org/z/oxbcE18TM
#include <memory> // / unique_ptr
#include <iostream>
#include <string>

using std::unique_ptr; using std::;
template<typename K, typename D> class Tree; // forward declaration
template<typename K, typename D>
class Node {
    friend Tree<K,D>; // allow access to private members
    K key;
    D data;
    unique_ptr<Node> left, right;
public:
    Node(const K& k, const D& d) : key(k), data(d) {}
};
template<typename K, typename D>
class Tree {
public:
    void insert(const K& key, const D& data);
    D* find(const K& key) const { return findRec(key, root); }
private:
    D* findRec(const K& key, const unique_ptr<Node<K,D>>& node);
    unique_ptr<Node<K,D>> root;
    void insert(const K& key, const D& data) {
        auto *current = &root;
        while (*current) // as long as unique_ptr contains something
            if (key < (*current)->key) {
                current = &(*current)->left;
            } else if (node.key < key) {
                current = &(*current)->right;
            }
    };
```