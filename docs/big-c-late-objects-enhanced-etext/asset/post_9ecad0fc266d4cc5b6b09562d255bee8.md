
Conversely, if you want to copy the directory tree, you start copying the root, because you need a target directory into which to place the children. This calls for preorder traversal.

![](img/d61019b035dd82beb581604273c0ee6b_838_0.png)

Note that pre- and postorder traversal can be defined for any trees, not just binary trees (see the sample code for this section). However, inorder traversal makes sense only for binary trees.

## 16.4.3 The Visitor Pattern

In the preceding sections, we simply printed each tree node that we visited. Often, we want to process the nodes in some other way. There is a “design pattern” (that is, a standard recipe to a commonly occurring problem), called the visitor pattern, that provides a solution. Define a class

```
class Visitor
{
public:
    virtual void visit(string data);
};
```

The preorder function receives an object of this class type, and calls its visit function:

```
void Tree::preorder(Visitor &v) const { preorder(root, v); }

void Tree::preorder(Node* n, Visitor& v) const
{
    if (n == nullptr) { return; }
    v.visit(n->data);
    for (Node* c : n->children) { preorder(c, v); }
}
```

Functions for postorder and, for a binary tree, inorder traversals can be implemented in the same way.

```
private:
    int counter = 0;
};

void ShortNameCounter::visit(string data)
{
    if (data.length() <= 5) { counter++; }
}

int ShortNameCounter::get() const
{
    return counter;
}

ShortNameCounter v2;
t1.preorder(v2);
cout << "Short names: " << v2.get() << endl;
```

Here, the visitor object accumulates the count. After the visit is complete, we can obtain the result.

## 16.4.4 Depth-First and Breadth-First Search

The traversals in the preceding sections are expressed using recursion. If you want to process the nodes of a tree, you supply a visitor, which is applied to all nodes. Sometimes, it is useful to use an iterative approach instead. Then you can stop processing nodes when a goal has been met.

To visit the nodes of a tree iteratively, we replace the recursive calls with a stack that keeps track of the children that need to be visited. Here is the algorithm:

- Push the root node on a stack.
- While the stack is not empty
- Pop the stack; let n be the popped node.
- Process n.
- Push the children of n on the stack, starting with the last one.

![](img/d61019b035dd82beb581604273c0ee6b_839_0.png)

© David Jones/iStockphoto.

*In a depth-first search, one moves as quickly as possible to the deepest nodes of the tree.*

Depth-first search uses a stack to track the nodes that it still needs to visit.

This algorithm is called depth-first search because it goes deeply into the tree and then backtracks when it reaches the leaves (see Figure 16). Note that the tree can be an arbitrary tree—it need not be binary.

![](img/d61019b035dd82beb581604273c0ee6b_839_1.png)

Figure 16 Depth-First Search

Breadth-first search first visits all nodes on the same level before visiting the children.

We push the children on the stack in right-to-left order so that the visit starts with the leftmost path. In this way, the nodes are visited in preorder. If the leftmost child had been pushed first, we would still have a depth-first search, just in a less intuitive order.

If we replace the stack with a queue, the visitation order changes. Instead of going deeply into the tree, we first visit all nodes at the same level before going on to the next level. This is called *breadth-first search* (Figure 17).

![](img/d61019b035dd82beb581604273c0ee6b_840_0.png)

Figure 17 Breadth-First Search

Here is the implementation of the breadth first algorithm:

```
void Tree::breadth_first(Visitor& v) const
{
    if (root == nullptr) { return; }
    queue<Node*> q;
    q.push(root);
    while (q.size() > 0)
    {
        Node* n = q.front();
        q.pop();
        v.visit(n->data);
        for (Node* c : n->children) { q.push(c); }
    }
}
```

For depth-first search, replace the queue with a stack (Exercise E16.10). Exercise E16.12 shows how to stop the search before all elements have been visited.

## 16.4.5 Tree Iterators

The C++ standard library uses trees to implement sets, and iterators to process the elements, like this:

```
set<string> t = . . .
set<string>::iterator iter = t.begin();
string first = *iter;
iter++;
. . .
```

It is easy to implement such an iterator with depth-first or breadth-first search. Make the stack or queue into a data member of the iterator object. The next function executes one iteration of the loop that you saw in the last section.

```
class BreadthFirstIterator
{
```

```
public:
  BreadthFirstIterator(Node* root);
  ...
  void next();
  ...
private:
  queue<Node*> q;
};

BreadthFirstIterator::BreadthFirstIterator(Node* root)
{
  if (root != nullptr) { q.push(root); }
}

void BreadthFirstIterator::next()
{
  Node* n = q.front();
  q.pop();
  for (Node* c : n->children) { q.push(c); }
}
```

Note that there is no visit function. The user of the iterator receives the node data, processes it, and decides whether to call next again.

This iterator produces the nodes in breadth-first order. For a binary search tree, one would want the nodes in sorted order instead. Exercise P16.9 shows how to implement such an iterator.

EXAMPLE CODE See sec04 of your companion code for a program that demonstrates preorder, postorder, and breadth-first traversal in a tree.

## 16.5 Red-Black Trees

As you saw in Section 16.3, insertion and removal in a binary search tree are O(log(n)) operations provided that the tree is balanced. In this section, you will learn about red-black trees, a special kind of binary search tree that rebalances itself after each insertion or removal. With red-black trees, we can guarantee efficiency of these operations. In fact, the standard C++ set and map classes also use red-black trees.

### 16.5.1 Basic Properties of Red-Black Trees

In a red-black tree, node coloring rules ensure that the tree is balanced.

A red-black tree is a binary search tree with the following additional properties:

- Every node is colored red or black.
- The root is black.
- A red node cannot have a red child (the “no double reds” rule).
- All paths from the root to a null ptr have the same number of black nodes (the “equal exit cost” rule).

Of course, the nodes aren't actually colored. Each node simply has a flag to indicate whether it is considered red or black. (The choice of these colors is traditional; one could have equally well used some other attributes. Perhaps, in an alternate universe, students learn about chocolate-vanilla trees.)

Figure 18 shows an example of a red-black tree.

![](img/d61019b035dd82beb581604273c0ee6b_842_0.png)

## Figure 18 A Red-Black Tree

Instead of thinking of the colors, imagine each node to be a toll booth. As you travel from the root to a nullptr (an exit), you have to pay $1 at each black toll booth, but the red toll booths are free. The cost of traveling along a path is the sum of the charges; that is, the number of black nodes on the path. The “equal exit cost” rule says that the cost of any trip that starts at the root and ends at an exit is the same, no matter which exit you choose.

![](img/d61019b035dd82beb581604273c0ee6b_842_1.png)

© Virginia Ni/Stockphoto.

Think of each node of a red-black tree as a toll booth. The total toll to each exit is the same.

Figures 19 and 20 show examples of trees that violate the “equal exit cost” and “no double reds” rules.

![](img/d61019b035dd82beb581604273c0ee6b_842_2.png)

## Figure 19 A Tree that Violates the “Equal Exit Cost” Rule

Note that the “equal exit cost” rule does not just apply to paths that end in a leaf, but to any path from the root to a node with one or two empty children. For example, in Figure 19, the path F–B violates the equal exit cost, yet B is not a leaf.

The “equal exit cost” rule eliminates highly unbalanced trees. You can’t have null pointers high up in the tree. In other words, the nodes that aren’t near the leaves need to have two children.

![](img/d61019b035dd82beb581604273c0ee6b_843_0.png)

## Figure 20 A Tree that Violates the “No Double Red” Rule

The “no double reds” rule gives some flexibility to add nodes without having to restructure the tree all the time. Some paths from the root to a null ptr can be a bit longer than others—by alternating red and black nodes—but none can be longer than twice the exit cost.

The cost of traveling on a path from a given node to a null ptr (that is, the number of black nodes on the path), is called the black height of the node. The cost of traveling from the root to a null ptr is called the black height of the tree.

A tree with given black height bh can’t be too sparse—it must have at least 2^{bh} − 1 nodes (see Exercise R16.18). Or, if we turn this relationship around,

2^{bh} − 1 ≤ n

2^{bh} ≤ n + 1

bh ≤ log₂(n + 1)

The “no double reds” rule says that the total height h of a tree is at most twice the black height:

h ≤ 2 · bh ≤ 2 · log₂(n + 1)

Therefore, traveling from the root to a null ptr is O(log(n)).

### 16.5.2 Insertion

To insert a new node into a red-black tree, first insert it as you would into a regular binary search tree (see Section 16.3.2). Note that the new node is a leaf.
