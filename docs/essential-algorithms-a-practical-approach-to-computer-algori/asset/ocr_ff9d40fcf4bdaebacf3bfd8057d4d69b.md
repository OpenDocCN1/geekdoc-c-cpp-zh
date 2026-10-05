an inorder traversal or reverse traversal more quickly is possible by using the branches alone.

![](bbox=[0.199, 0.142, 0.506, 0.313])

> NOTE You can define other threads in a tree, but this type is the most common. Because it includes threads forward and backward through the tree's inorder traversal, this kind of tree is sometimes called a symmetrically threaded tree.

> NOTE Notice that all the nodes in Figure 10-12 have either a left branch or a right branch. You can use the same references for both branches and threads if you can somehow distinguish between them. For example, if you use the node class two boolean variables, HasLeftBranch and HasRightBranch, you can store threads in the child links if you set those variables to True.

You can pack the two boolean values into a byte and use byte operations to see if they are.
In practice, saving in memory may not be worth the extra complexity and potential confusion you're working with an extremely large tree.

To use this kind of threaded tree, you need to know two things: how to build the tree and how to traverse it.

# Building Threaded Trees

A threaded tree starts with a single node that has no branches and threads set to null. Creating node is simple.
The trick is adding a new node to the tree. There are two cases, depending on whether you add the new node as the left or right child of its parent.
First, suppose you're adding the new node as a left child. Suppose you're adding the node 3 as the left child of node 4 in the tree shown in Figure 10-12. Because of where the new node is placed, its value is the next smaller value compared to its parent's value. (In this example, 3 is the next smaller value after 4.)