![](bbox=[0.04, 0.07, 0.92, 0.34])

# Figure 10.18 Example of a B⁺-tree of order four. Internal nodes must store between two and four children. For this example, the record size is assumed to be such that leaf nodes store between three and five records.

to form a doubly linked list. Thus, the entire collection of records can be traversed in sorted order by visiting all the leaf nodes on the linked list. Here is a C++-like pseudocode representation for the B⁺-tree node class. Leaf node and internal node subclasses would implement this base class.

```
// Abstract class definition for B+-trees
template <typename Key, typename E>class BPNode {
public:
    BPNode* lftptr;  BPNode* rgtptr; // Links to siblings
    virtual ~BPNode() {} // Base destructor
    virtual bool isLeaf() const =0;  // True if node is a leaf
    virtual bool isFull() const =0;  // True if node is full
    virtual int numrecs() const =0;  // Current num of records
    virtual Key* keys() const=0;     // Return array of keys
};
```

An important implementation detail to note is that while Figure 10.17 shows internal nodes containing three keys and four pointers, class BPNode is slightly different in that it stores key/pointer pairs. Figure 10.17 shows the B⁺-tree as it is traditionally drawn. To simplify implementation in practice, nodes really do associate a key with each pointer. Each internal node should be assumed to hold in the leftmost position an additional key that is less than or equal to any possible key value in the node’s leftmost subtree. B⁺-tree implementations typically store an additional dummy record in the leftmost leaf node whose key value is less than any legal key value.

B⁺-trees are exceptionally good for range queries. Once the first record in the range has been found, the rest of the records with keys in the range can be accessed by sequential processing of the remaining records in the first node, and then continuing down the linked list of leaf nodes as far as necessary. Figure 10.18 illustrates the B⁺-tree.