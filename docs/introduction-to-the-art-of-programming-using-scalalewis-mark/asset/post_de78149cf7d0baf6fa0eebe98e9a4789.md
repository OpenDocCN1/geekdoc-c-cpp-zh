
ImmutableTreeMap is invariant on type parameter K. This is a concept that is covered in appendix B, but what matters here is that there is no type that we can pick that will work for all key types. This could lead to significant wasted memory if every leaf of every tree referred to a different instance of Empty. Indeed, in that situation, the empties would take nearly as much memory as the rest of the trees. However, as this code is written, every tree that is made with the apply method of the ImmutableTreeMap object makes a single Empty object and that is shared as the terminator for everything in that tree, even as more elements are added and the number of leaves grows. The fact that both Node and Empty are private means that the apply method is the only way to instantiate one of these trees.

Another difference between this tree and the last one is that this tree requires K <: Ordered[K] instead of passing in a comparator. This is because each node in an immutable tree is a fully functional and independent tree of its own. Using a comparator function would require that all nodes keep a reference to that function. That is an overhead that we would rather avoid if possible. This was not an issue for the mutable BST as many nodes existed in each tree and only the enclosing tree needed to keep track of the comparator.

The immutable tree does have somewhat higher overhead for modifying operations. However, the overall performance is still O(log(n)). The difference is that any time nodes are added or changed, everything must be replaced on the path from that node to the root. That allows any earlier versions of the tree to remain intact. So the immutable BST not only does O(log(n)) comparisons and memory reads for the + and - operations, it also creates O(log(n)) new nodes for those operations. This is still far superior to the O(n) nodes that have to be created for random modifications of immutable lists.

## 29.4 End of Chapter Material

### 29.4.1 Summary of Concepts

- A tree is a structure with nodes and edges that go from one node to another. All nodes have exactly one incoming edge except the root which has none.
- The terminology for describing trees is a combination of genealogical and biological.
  - Parent node has an edge that refers to the child node.
  - Children of the same parent are called siblings.
  - Everything below a node are called descendants while those in line above are called ancestors.
  - Nodes with no children are called leaves.
  - Number of edges down from the root is called the depth.
  - Number of edges up from lowest leaf is called the height.
  - Number of descendants plus self is the size of a node.
- There are multiple ways to traverse a tree.
  - Depth first traversals handle the children before they handle later siblings.
    - Work well with recursion.
    - Pre-order: Handle a node before the children.
    - Post-order: Handle a node after the children.
    - In-order: Handle a node between the children. This makes most sense for trees limited to two children per node.
  - Breadth-first traversal runs across an entire generation before going to the next one. This needs to be implemented with a loop and a queue.
- A tree makes a convenient way of representing a parsed formula. The recursive parsing code written earlier can be easily modified to produce this structure. The tree structure allows much faster evaluation than reparsing the string.
- A binary search tree, BST, is an efficient structure for storing values when there is a complete ordering on some key type.
  - Each node in a BST can have a left child and/or a right child.
  - The key of the left child must be smaller than the key of the parent and the key of the right child must be greater than the key of the parent.
  - Getting, adding, and removing from a balanced tree can all be done in $O(\log(n))$ operations.
  - A standard BST can degrade to a linked list. Such highly unbalanced trees give $O(n)$ behavior.

### 29.4.2 Exercises

1. Test the relative speed of the recursive parsing evaluation method we wrote in the last chapter to that with the tree built in this chapter. Modify the code from the last chapter to include variables and call the function on a formula a sufficient number of times to see your machine pause. Repeat the same thing using the tree version from this chapter, but build one `Formula` object and do the evaluations with different variable values.
2. Add a method to the formula node that will return a simplified version of that node. Simplification should include the following:

   - Addition with zero simplifies to the other value.
   - Subtracting zero simplifies to the other value.
   - Multiplication by one simplifies to the other value.
   - Division by one simplifies to the other value.
   - Multiplication by zero simplifies to zero.
   - Division with a zero numerator simplifies to zero.
   - Any operation between two numbers can become a number with the result.

   Write the code recursively so that the simplification happens after recursion when the stack pops back up so that when a node is simplified, it takes into account the simplified children.

   For a bit of an extra challenge, you could try to identify other simplifications and implement them as well.

3. Add a method to the formula node that will return the derivative of that node. Given the operations we have, this should require little more than remembering the product rule and the quotient rule.
4. Combine exercises 2 and 3 so that you have a derivative method that simplifies the expression as far as possible.
5. Alter the -= method of the TreeMap so that it is not recursive and only reassigns references when a child node actually changes. Make sure to test your code to insure that you have dealt with all possible cases. Once you feel confident it works, compare the complexity of the code and the execution speed to the recursive solution.

### 29.4.3 Projects

1. If you are writing a MUD, you should use a BST-based map for finding rooms by unique names.
2. If you are writing the web spider, make a site tree and display it graphically. Allow the user to specify what page to use as the root. Link in other pages so that depth is the minimum click count from the root. If a page can be reached in the same click count from the root, favor the one that occurred earlier in the page of lowest depth.
3. If you are writing a graphical game, use a BST-based map as a way for you to quickly look up or jump to different elements of your game.
4. If you are doing the math worksheet, this chapter provides you with the ability to parse your formulas to an evaluation tree, which can make processing a lot faster. You can also use the tree as a means of doing symbolic manipulation. You will want to have simplification for this to work, but you can easily write code to take the derivative of a tree and produce a new tree. With a bit more effort, you can write code to do anti-derivatives/indefinite integrals for some functions. Note that not all functions have anti-derivatives with a closed form so some things simply won’t work. If you are looking for even more of a challenge, try to do symbolic definite integrals and simplify them in a way that makes reasonable sense.
5. The expression trees can also be used to good effect in a Photoshop® program. You can give the user the ability to make custom filters by specifying a function that is used to combine the colors in pixels around the current pixel. Given the number of pixels in any real image, this would have been unacceptably slow with our earlier String parsing evaluation. The tree-based evaluation makes it feasible. You can decide what syntax you will have the user use to specify different adjacent pixel Red, Green, Blue (RGB) values.
6. Fast evaluation of user-entered formulas also provides a significant benefit for the simulation workbench project. You can use custom forces to specify force functions for particle interactions, or as part of random number generation for discrete event simulations.
