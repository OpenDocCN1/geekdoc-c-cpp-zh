
```
/usr
    mark
        book
            ch1.r
            ch2.r
            ch3.r
        course
            cop3530
                fall
                    syl.r
                spr
                    syl.r
                sum
                    syl.r
            junk
    alex
        junk
    bill
        work
            course
                cop3212
                    fall
                        grades
                            prog1.r
                            prog2.r
                    fall
                        prog2.r
                        prog1.r
                        grades
```

**Figure 4.7** The (preorder) directory listing

node. Furthermore, line 4 can be executed at most once for each child of each node. But the number of children is exactly one less than the number of nodes. Finally, the for loop iterates once per execution of line 4 plus once each time the loop ends. Thus, the total amount of work is constant per node. If there are N file names to be output, then the running time is O(N).

Another common method of traversing a tree is the postorder traversal. In a postorder traversal, the work at a node is performed after (post) its children are evaluated. As an example, Figure 4.8 represents the same directory structure as before, with the numbers in parentheses representing the number of disk blocks taken up by each file.

Since the directories are themselves files, they have sizes too. Suppose we would like to calculate the total number of blocks used by all the files in the tree. The most natural way to do this would be to find the number of blocks contained in the subdirectories /usr/mark (30), /usr/alex (9), and /usr/bill (32). The total number of blocks is then the total in the

![](img/e449061a0cac9cafaefd979fab665b33_144_0.png)

**Figure 4.8** Unix directory with file sizes obtained via postorder traversal

```
int FileSystem::size() const
{
    int totalSize = sizeOfThisFile( );

    if( isDirectory( ) )
        for each file c in this directory ( for each child )
            totalSize += c.size( );

    return totalSize;
}
```

**Figure 4.9** Pseudocode to calculate the size of a directory

subdirectories (71) plus the one block used by /usr, for a total of 72. The pseudocode method size in Figure 4.9 implements this strategy.

If the current object is not a directory, then size merely returns the number of blocks it uses in the current object. Otherwise, the number of blocks used by the directory is added to the number of blocks (recursively) found in all the children. To see the difference between the postorder traversal strategy and the preorder traversal strategy, Figure 4.10 shows how the size of each directory or file is produced by the algorithm.

## 4.2 Binary Trees

A binary tree is a tree in which no node can have more than two children.

Figure 4.11 shows that a binary tree consists of a root and two subtrees, $T_L$ and $T_R$, both of which could possibly be empty.

A property of a binary tree that is sometimes important is that the depth of an average binary tree is considerably smaller than N. An analysis shows that the average depth is $O(\sqrt{N})$, and that for a special type of binary tree, namely the *binary search tree*, the average value of the depth is $O(\log N)$. Unfortunately, the depth can be as large as $N - 1$, as the example in Figure 4.12 shows.

| File/Directory | Blocks |
|----------------|--------|
| ch1.r | 3 |
| ch2.r | 2 |
| ch3.r | 4 |
| book | 10 |
| syl.r | 1 |
| fall | 2 |
| syl.r | 5 |
| spr | 6 |
| syl.r | 2 |
| sum | 3 |
| cop3530 | 12 |
| course | 13 |
| junk | 6 |
| mark | 30 |
| junk | 8 |
| alex | 9 |
| work | 1 |
| grades | 3 |
| prog1.r | 4 |
| prog2.r | 1 |
| fall | 9 |
| prog2.r | 2 |
| prog1.r | 7 |
| grades | 9 |
| fall | 19 |
| cop3212 | 29 |
| course | 30 |
| bill | 32 |
| /usr | 72 |

**Figure 4.10** Trace of the size function

![](img/e449061a0cac9cafaefd979fab665b33_145_0.png)

**Figure 4.11** Generic binary tree

![](img/e449061a0cac9cafaefd979fab665b33_146_0.png)

**Figure 4.12** Worst-case binary tree

### 4.2.1 Implementation

Because a binary tree node has at most two children, we can keep direct links to them. The declaration of tree nodes is similar in structure to that for doubly linked lists, in that a node is a structure consisting of the element information plus two pointers (left and right) to other nodes (see Fig. 4.13).

We could draw the binary trees using the rectangular boxes that are customary for linked lists, but trees are generally drawn as circles connected by lines, because they are actually graphs. We also do not explicitly draw nullPtr links when referring to trees, because every binary tree with N nodes would require N + 1 nullPtr links.

Binary trees have many important uses not associated with searching. One of the principal uses of binary trees is in the area of compiler design, which we will now explore.

### 4.2.2 An Example: Expression Trees

Figure 4.14 shows an example of an expression tree. The leaves of an expression tree are operands, such as constants or variable names, and the other nodes contain operators. This particular tree happens to be binary, because all the operators are binary, and although this is the simplest case, it is possible for nodes to have more than two children. It is also possible for a node to have only one child, as is the case with the unary minus operator. We can evaluate an expression tree, T, by applying the operator at the root to the values

```
struct BinaryNode
{
    Object      element;   // The data in the node
    BinaryNode *left;      // Left child
    BinaryNode *right;     // Right child
};
```

**Figure 4.13** Binary tree node class (pseudocode)

![](img/e449061a0cac9cafaefd979fab665b33_147_0.png)

**Figure 4.14** Expression tree for (a + b * c) + ((d + e + f) * g)

obtained by recursively evaluating the left and right subtrees. In our example, the left subtree evaluates to a + (b * c) and the right subtree evaluates to ((d + e) * f) * g. The entire tree therefore represents (a + (b * c)) + (((d + e) + f) * g).

We can produce an (overly parenthesized) infix expression by recursively producing a parenthesized left expression, then printing out operator at the root, and finally recursively producing a parenthesized right expression. This general strategy (left, node, right) is known as an inorder traversal; it is easy to remember because of the type of expression it produces.

An alternate traversal strategy is to recursively print out the left subtree, the right subtree, and then the operator. If we apply this strategy to our tree above, the output is a b c * + d e f + + * g *, which is easily seen to be the postfix representation of Section 3.6.3.

This traversal strategy is generally known as a postorder traversal. We have seen this traversal strategy earlier in Section 4.1.

A third traversal strategy is to print out the operator first and then recursively print out the left and right subtrees. The resulting expression, ++ + a * b c * + * d e f g, is the less useful prefix notation, and the traversal strategy is a preorder traversal, which we have also seen earlier in Section 4.1. We will return to these traversal strategies later in the chapter.

### Constructing an Expression Tree

We now give an algorithm to convert a postfix expression into an expression tree. Since we already have an algorithm to convert infix to postfix, we can generate expression trees from the two common types of input. The method we describe strongly resembles the postfix evaluation algorithm of Section 3.6.3. We read our expression one symbol at a time. If the symbol is an operand, we create a one-node tree and push a pointer to it onto a stack. If the symbol is an operator, we pop (pointers) to two trees T1 and T2 from the stack (T1 is popped first) and form a new tree whose root is the operator and whose left and right children point to T2 and T1, respectively. A pointer to this new tree is then pushed onto the stack.

As an example, suppose the input is

```
a b + c d e + * *
```

The first two symbols are operands, so we create one-node trees and push pointers to them onto a stack.²

![](img/e449061a0cac9cafaefd979fab665b33_148_0.png)

Next, a + is read, so two pointers to trees are popped, a new tree is formed, and a pointer to it is pushed onto the stack.

![](img/e449061a0cac9cafaefd979fab665b33_148_1.png)

Next, c, d, and e are read, and for each a one-node tree is created and a pointer to the corresponding tree is pushed onto the stack.

![](img/e449061a0cac9cafaefd979fab665b33_148_2.png)

Now a + is read, so two trees are merged.
