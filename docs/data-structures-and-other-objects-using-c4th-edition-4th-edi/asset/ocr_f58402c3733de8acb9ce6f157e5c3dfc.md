Another form of balanced tree—the AVL tree—is sometimes used for the STL map or multimap. It is named after its inventors, the Russian mathematicians Georgy Adelson-Velsky and Yevgeny Landis, who published their results in 1962.

# CHAPTER SUMMARY

+   - A heap is a complete binary tree that follows the rule that the entry at any node is never less than any of its children’s entries. Heaps provide an efficient implementation of priority queues.
+   - The STL includes a priority queue class as well as algorithms for building and manipulating heaps.
+   - A B-tree is a tree for storing entries in a manner that follows six rules. The first two rules specify the minimum and maximum number of entries for each node. The third rule requires each node’s entries to be sorted from smallest to largest. Rules 4 and 5 indicate how many subtrees a nonleaf node must have and impose an order on the elements of the subtrees. The last rule requires each leaf to be at the same depth.
+   - The tree algorithms that we have seen for binary search trees, heaps, and B-trees all have worst-case time performance of O(d), where d is the depth of the tree.
+   - The depth of a heap or B-tree is never more than O(log n), where n is the number of nodes. Hence, the operations on these structures are also O(log n).
+   - The STL includes two classes, map and multimap, which allow a programmer to store key/value pairs.

# Solutions to Self-Test Exercises

+   1. Heaps are always complete binary trees. In addition, the ordering rule is different, requiring that an entry contained at a node is never less than the entries of the node’s children.
+   2. The priority queue class needs a private member variable that is an array of objects that can be compared with a less-than operator. Our solution is based on the interface from Figure 8.12 on page 427. Here is the solution with a fixed-sized array:
+   template <class Item>
+   class simple_priority_queue

```
{
    public:
    // TYPEDEFS and MEMBER CONSTANT
    typedef Item value_type;
    typedef std::size_t size_type;
    static const size_type CAPACITY=50;
    // CONSTRUCTOR
    priority_queue( );
    // MODIFICATION MEMBER FUNCTIONS
    void pop( );
    void push(const Item& entry);
    // CONSTANT MEMBER FUNCTIONS
    bool empty( ) const;
    size_type size( ) const;
    Item top( ) const;
}
```