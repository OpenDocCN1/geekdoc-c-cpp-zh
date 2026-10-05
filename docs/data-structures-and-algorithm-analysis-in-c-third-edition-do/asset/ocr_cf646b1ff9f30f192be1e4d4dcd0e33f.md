```
// HuffmanTree is a template of two parameters: the element
// type being coded and a comparator for two such elements
template <typename E>
class HuffmanTree {
private:
    HuffNode<E>* Root; // Tree root
public:
    HuffTree(E val, int freq) // Leaf constructor
    { Root = new HuffNode<E>(val, freq); }
    // Internal node constructor
    HuffTree(HuffTree<E>* r)
    { Root = new HuffNode<E>(r->root(), r->root()); } // Destructor
    ~HuffTree() { root(); } // Destructor
HuffNode<E>* root() { return Root; } // Get root
    int weight() { return Root->weight(); } // Root weight
};
```

Figure 5.28 Class declarations for the Huffman tree.

```
// Build a Huffman tree from a collection of frequencies
template <typename E> HuffmanTree<E>*
buildHuff(HuffmanTree<E>>** heapArray, int count) {
    HuffmanTree<E>**, minTreeComp* forest =
        new HuffmanTree<E>**, minTreeComp* forest (heapArray,
                                            count, count);
    HuffmanTree *temp1, *temp2, *temp3 = NULL;
    while (forest->size() > 1) { // Pull first two trees
        temp2 = forest->removeFirst(); // off the list
        temp1 = forest->removeFirst();
        temp3 = new HuffmanTree(temp1, temp2); // Put the new tree back on list
        forest->insert(temp3); // Must delete the remnants
        delete temp1; // of the trees created
        delete temp2;
    }
    return temp3;
}
```

Figure 5.29 Implementation for the Huffman tree construction function.
buildHuff takes input fl, the min-heap of partial Huffman trees, which
initially are single leaf nodes as shown in Step 1 of Figure 5.25. The body of
function buildTree consists mainly of a for loop. On each iteration of the
loop, the first two trees are taken off the heap and placed in variables
templ and temp2. A tree is created (temp3) such that the left and right subtrees
templ1 and temp2, respectively. Finally, temp3 is returned to fl.