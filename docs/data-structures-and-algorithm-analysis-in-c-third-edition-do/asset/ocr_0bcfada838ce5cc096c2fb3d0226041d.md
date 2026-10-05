# Sec. 5.3 Binary Tree Implementations

```
// Simple binary tree node implementation
template <typename Key, typename E>
class BSTNode : public BinNode<E> {
private:
    Key k;                               // The node's key
    E e;                                // The node's value
    BSTNode* lc;                        // Pointer to left child
    BSTNode* rc;                        // Pointer to right child

public:
    // Two constructors - with and without initial values
    BSTNode(Key K, E e, lc = NULL, BSTNode* r = NULL)
    { k = K; e = e; lc = lc; rc = r; }
    ~BSTNode() {}                       // Destructor

    // Functions to set and return the key
    E& element() { return e; }
    void setElement(const E& e) { e = e; }
    Key key() { return k; }
    void setKey(const Key& K) { k = K; }

    // Functions to set and return the children
    inline BSTNode* left() const { return lc; }
    void setLeft(BinNode<E>* b) { lc = (BSTNode*)b; }
    inline BSTNode* right() const { return rc; }
    void setRight(BinNode<E>* b) { rc = (BSTNode*)b; }

    // Return true if it is a leaf, false otherwise
    bool isLeaf() { return (lc == NULL) && (rc == NULL); }
};
```

**Figure 5.7** A binary tree class implementation.

![](bbox=[0.273, 0.655, 0.726, 0.829])

**Figure 5.8** Illustration of a typical pointer-based binary tree implementation, where each node stores two pointers and a value.