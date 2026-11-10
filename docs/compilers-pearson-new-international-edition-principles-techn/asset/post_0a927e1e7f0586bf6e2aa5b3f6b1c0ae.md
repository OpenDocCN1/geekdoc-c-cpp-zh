
## 6.1. VARIANTS OF SYNTAX TREES

### 6.1.1 Directed Acyclic Graphs for Expressions

Like the syntax tree for an expression, a DAG has leaves corresponding to atomic operands and interior nodes corresponding to operators. The difference is that a node N in a DAG has more than one parent if N represents a common subexpression; in a syntax tree, the tree for the common subexpression would be replicated as many times as the subexpression appears in the original expression. Thus, a DAG not only represents expressions more succinctly, it gives the compiler important clues regarding the generation of efficient code to evaluate the expressions.

**Example 6.1:** Figure 6.3 shows the DAG for the expression

\(a + a * (b − c) + (b − c) * d\)

The leaf for a has two parents, because a appears twice in the expression. More interestingly, the two occurrences of the common subexpression b−c are represented by one node, the node labeled −. That node has two parents, representing its two uses in the subexpressions a*(b−c) and (b−c)*d. Even though b and c appear twice in the complete expression, their nodes each have one parent, since both uses are in the common subexpression b−c. □

![](img/2a44b9071782fade81f3050c3b718341_363_0.png)

Figure 6.3: DAG for the expression \(a + a * (b − c) + (b − c) * d\)

The SDD of Fig. 6.4 can construct either syntax trees or DAGs. It was used to construct syntax trees in Example 5.11, where functions *Leaf* and *Node* created a fresh node each time they were called. It will construct a DAG if, before creating a new node, these functions first check whether an identical node already exists. If a previously created identical node exists, the existing node is returned. For instance, before constructing a new node, *Node(op, left, right)*, we check whether there is already a node with label *op*, and children *left* and *right*, in that order. If so, *Node* returns the existing node; otherwise, it creates a new node.

| Production | Semantic Rules |
|---|---|
| 1) \(E \rightarrow E_1 + T\) | \(E.node = new Node('+', E_1.node, T.node)\) |
| 2) \(E \rightarrow E_1 - T\) | \(E.node = new Node('-', E_1.node, T.node)\) |
| 3) \(E \rightarrow T\) | \(E.node = T.node\) |
| 4) \(T \rightarrow ( E )\) | \(T.node = E.node\) |
| 5) \(T \rightarrow id\) | \(T.node = new Leaf(id, id.entry)\) |
| 6) \(T \rightarrow num\) | \(T.node = new Leaf(num, num.val)\) |

Figure 6.4: Syntax-directed definition to produce syntax trees or DAGs

**Example 6.2:** The sequence of steps shown in Fig. 6.5 constructs the DAG in Fig. 6.3, provided *Node* and *Leaf* return an existing node, if possible, as discussed above. We assume that entry-a points to the symbol-table entry for a, and similarly for the other identifiers.

- 1. \(p_1 = Leaf(id, entry-a)\)
- 2. \(p_2 = Leaf(id, entry-a) = p_1\)
- 3. \(p_3 = Leaf(id, entry-b)\)
- 4. \(p_4 = Leaf(id, entry-c)\)
- 5. \(p_5 = Node('-', p_3, p_4)\)
- 6. \(p_6 = Node('*', p_1, p_5)\)
- 7. \(p_7 = Node('+', p_1, p_6)\)
- 8. \(p_8 = Leaf(id, entry-b) = p_3\)
- 9. \(p_9 = Leaf(id, entry-c) = p_4\)
- 10. \(p_{10} = Node('-', p_3, p_4) = p_5\)
- 11. \(p_{11} = Leaf(id, entry-d)\)
- 12. \(p_{12} = Node('*', p_5, p_{11})\)
- 13. \(p_{13} = Node('+', p_7, p_{12})\)

Figure 6.5: Steps for constructing the DAG of Fig. 6.3

When the call to \(Leaf(id, entry-a)\) is repeated at step 2, the node created by the previous call is returned, so \(p_2 = p_1\). Similarly, the nodes returned at steps 8 and 9 are the same as those returned at steps 3 and 4 (i.e., \(p_8 = p_3\) and \(p_9 = p_4\)). Hence the node returned at step 10 must be the same as that returned at step 5; i.e., \(p_{10} = p_5\). □

### 6.1.2 The Value-Number Method for Constructing DAGs

Often, the nodes of a syntax tree or DAG are stored in an array of records, as suggested by Fig. 6.6. Each row of the array represents one record, and therefore one node. In each record, the first field is an operation code, indicating the label of the node. In Fig. 6.6(b), leaves have one additional field, which holds the lexical value (either a symbol-table pointer or a constant, in this case), and interior nodes have two additional fields indicating the left and right children.

![](img/2a44b9071782fade81f3050c3b718341_365_0.png)

Figure 6.6: Nodes of a DAG for `i = i + 10` allocated in an array

In this array, we refer to nodes by giving the integer index of the record for that node within the array. This integer historically has been called the *value number* for the node or for the expression represented by the node. For instance, in Fig. 6.6, the node labeled `+` has value number 3, and its left and right children have value numbers 1 and 2, respectively. In practice, we could use pointers to records or references to objects instead of integer indexes, but we shall still refer to the reference to a node as its “value number.” If stored in an appropriate data structure, value numbers help us construct expression DAGs efficiently; the next algorithm shows how.

Suppose that nodes are stored in an array, as in Fig. 6.6, and each node is referred to by its value number. Let the *signature* of an interior node be the tuple ⟨op, l, r⟩, where op is the label, l its left child’s value number, and r its right child’s value number. A unary operator may be assumed to have r = 0.

### Algorithm 6.3: The value-number method for constructing the nodes of a DAG.

**INPUT:** Label `op`, node `l`, and node `r`.

**OUTPUT:** The value number of a node in the array with signature ⟨op, l, r⟩.

**METHOD:** Search the array for a node `M` with label `op`, left child `l`, and right child `r`. If there is such a node, return the value number of `M`. If not, create in the array a new node `N` with label `op`, left child `l`, and right child `r`, and return its value number.

While Algorithm 6.3 yields the desired output, searching the entire array every time we are asked to locate one node is expensive, especially if the array holds expressions from an entire program. A more efficient approach is to use a hash table, in which the nodes are put into “buckets,” each of which typically will have only a few nodes. The hash table is one of several data structures that support *dictionaries* efficiently.¹ A dictionary is an abstract data type that allows us to insert and delete elements of a set, and to determine whether a given element is currently in the set. A good data structure for dictionaries, such as a hash table, performs each of these operations in time that is constant or close to constant, independent of the size of the set.

¹ See Aho, A. V., J. E. Hopcroft, and J. D. Ullman, *Data Structures and Algorithms*, Addison-Wesley, 1983, for a discussion of data structures supporting dictionaries.

To construct a hash table for the nodes of a DAG, we need a *hash function* h that computes the index of the bucket for a signature ⟨op,l,r⟩, in a way that distributes the signatures across buckets, so that it is unlikely that any one bucket will get much more than a fair share of the nodes. The bucket index h(op,l,r) is computed deterministically from op, l, and r, so that we may repeat the calculation and always get to the same bucket index for node ⟨op,l,r⟩.

The buckets can be implemented as linked lists, as in Fig. 6.7. An array, indexed by hash value, holds the *bucket headers*, each of which points to the first cell of a list. Within the linked list for a bucket, each cell holds the value number of one of the nodes that hashes to that bucket. That is, node ⟨op,l,r⟩ can be found on the list whose header is at index h(op,l,r) of the array.

![](img/2a44b9071782fade81f3050c3b718341_366_0.png)

Thus, given the input node op, l, and r, we compute the bucket index h(op,l,r) and search the list of cells in this bucket for the given input node. Typically, there are enough buckets so that no list has more than a few cells. We may need to look at all the cells within a bucket, however, and for each value number v found in a cell, we must check whether the signature ⟨op,l,r⟩ of the input node matches the node with value number v in the list of cells (as in Fig. 6.7). If we find a match, we return v. If we find no match, we know no such node can exist in any other bucket, so we create a new cell, add it to the list of cells for bucket index h(op,l,r), and return the value number in that new cell.

### 6.1.3 Exercises for Section 6.1

- **Exercise 6.1.1:** Construct the DAG for the expression \(((x + y) − ((x + y) ∗ (x − y))) + ((x + y) ∗ (x − y))\)
