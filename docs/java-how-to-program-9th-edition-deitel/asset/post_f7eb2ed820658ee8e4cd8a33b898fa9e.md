
Figure 22.13 creates a Queue<T> class that contains a List<T> (Fig. 22.3) object and provides methods enqueue, dequeue, isEmpty and print. Class List<T> contains some methods (e.g., insertAtFront and removeFromBack) that we’d rather not make accessible through Queue<T>’s public interface. Using composition enables us to hide class List<T>’s other public methods from clients of class Queue<T>. Each Queue<T> method calls an appropriate List<T> method—method enqueue calls List<T> method insertAtBack, method dequeue calls List<T> method removeFromFront, method isEmpty calls List<T> method isEmpty and method print calls List<T> method print. For reuse, class Queue<T> is declared in package com.deitel.ch22.

Class QueueTest’s (Fig. 22.14) main method creates and initializes Queue<T> variable queue (line 10). Lines 13, 15, 17 and 19 enqueue four integers, taking advantage of auto-boxing to insert Integer objects into the queue. Lines 27–32 use an infinite loop to dequeue the objects in first-in, first-out order. When the queue is empty, method dequeue throws an EmptyListException, and the program displays the exception’s stack trace.

```
// Fig. 22.13: Queue.java
// Queue uses class List.
package com.deitel.ch22;

public class Queue<T>
{
    private List<T> queueList;

    // no-argument constructor
    public Queue()
    {
        queueList = new List<T>("queue");
    } // end Queue no-argument constructor

    // add object to queue
    public void enqueue(T object)
    {
        queueList.insertAtBack(object);
    } // end method enqueue

    // remove object from queue
    public T dequeue() throws EmptyListException
    {
        return queueList.removeFromFront();
    } // end method dequeue

    // determine if queue is empty
    public boolean isEmpty()
    {
        return queueList.isEmpty();
    } // end method isEmpty

    // output queue contents
    public void print()
    {
        queueList.print();
    } // end method print
} // end class Queue
```

Fig. 22.13 | Queue uses class List.

// Fig. 22.14: QueueTest.java
// Class QueueTest.
import com.deitel.ch22.Queue;
import com.deitel.ch22.EmptyListException;

public class QueueTest
{
    public static void main( String[] args )
    {
        Queue< Integer > queue = new Queue< Integer >();

        // use enqueue method
        queue.enqueue( -1 );
        queue.print();
        queue.enqueue( 0 );
        queue.print();
        queue.enqueue( 1 );
        queue.print();
        queue.enqueue( 5 );
        queue.print();

        // remove objects from queue
        try
        {
            int removedItem;

            while ( true )
            {
                removedItem = queue.dequeue(); // use dequeue method
                System.out.printf( "%n%d dequeued%n", removedItem );
                queue.print();
            } // end while
        } // end try
        catch ( EmptyListException emptyListException )
        {
            emptyListException.printStackTrace();
        } // end catch
    } // end main
} // end class QueueTest
```

The queue is: -1
The queue is: -1 0
The queue is: -1 0 1
The queue is: -1 0 1 5

-1 dequeued
The queue is: 0 1 5

Fig. 22.14 | Queue processing program. (Part I of 2.)

0 dequeued
The queue is: 1 5

1 dequeued
The queue is: 5

5 dequeued
Empty queue
com.deitel.ch22.EmptyListException: queue is empty
    at com.deitel.ch22.List.removeFromFront(List.java:81)
    at com.deitel.ch22.Queue.dequeue(Queue.java:24)
    at QueueTest.main(QueueTest.java:29)

Fig. 22.14 | Queue processing program. (Part 2 of 2.)

## 22.7 Trees

Lists, stacks and queues are linear data structures (i.e., sequences). A tree is a nonlinear, two-dimensional data structure with special properties. Tree nodes contain two or more links. This section discusses binary trees (Fig. 22.15)—trees whose nodes each contain two links (one or both of which may be null). The root node is the first node in a tree. Each link in the root node refers to a child. The left child is the first node in the left subtree (also known as the root node of the left subtree), and the right child is the first node in the right subtree (also known as the root node of the right subtree). The children of a specific node are called siblings. A node with no children is called a leaf node. Computer scientists normally draw trees from the root node down—the opposite of the way most trees grow in nature.

![](img/009e962758dcc71dbc43a493362e6dc0_961_0.png)

Fig. 22.15 | Binary tree graphical representation.

In our example, we create a special binary tree called a binary search tree. A binary search tree (with no duplicate node values) has the characteristic that the values in any left subtree are less than the value in that subtree’s parent node, and the values in any right subtree are greater than the value in that subtree’s parent node. Figure 22.16 illustrates a binary search tree with 12 integer values. The shape of the binary search tree that corresponds to a set of data can vary, depending on the order in which the values are inserted into the tree.

![](img/009e962758dcc71dbc43a493362e6dc0_962_0.png)

Fig. 22.16 | Binary search tree containing 12 values.

Figures 22.17 and 22.18 create a generic binary search tree class and use it to manipulate a tree of integers. The application in Fig. 22.18 traverses the tree (i.e., walks through all its nodes) three ways—using recursive inorder, preorder and postorder traversals. The program generates 10 random numbers and inserts each into the tree. Class Tree<T> is declared in package com.deitel.ch22 for reuse.

// Fig. 22.17: Tree.java
// TreeNode and Tree class declarations for a binary search tree.
package com.deitel.ch22;

// class TreeNode definition
class TreeNode< T extends Comparable< T > >
{
    // package access members
    TreeNode< T > leftNode; // left node
    T data; // node value
    TreeNode< T > rightNode; // right node

    // constructor initializes data and makes this a leaf node
    public TreeNode( T nodeData )
    {
        data = nodeData;
        leftNode = rightNode = null; // node has no children
    } // end TreeNode constructor

    // locate insertion point and insert new node; ignore duplicate values
    public void insert( T insertValue )
    {
        // insert in left subtree
        if ( insertValue.compareTo( data ) < 0 )
        {
            // insert new TreeNode
            if ( leftNode == null )
                leftNode = new TreeNode< T >( insertValue );
            else // continue traversing left subtree recursively
                leftNode.insert( insertValue );
        } // end if

        // insert in right subtree
        else if ( insertValue.compareTo( data ) > 0 )
        {
            // insert new TreeNode
            if ( rightNode == null )
                rightNode = new TreeNode< T >( insertValue );
            else // continue traversing right subtree recursively
                rightNode.insert( insertValue );
        } // end else if
    } // end method insert
} // end class TreeNode

// class Tree definition
public class Tree< T extends Comparable< T > >
{
    private TreeNode< T > root;

    // constructor initializes an empty Tree of integers
    public Tree()
    {
        root = null;
    } // end Tree no-argument constructor

    // insert a new node in the binary search tree
    public void insertNode( T insertValue )
    {
        if ( root == null )
            root = new TreeNode< T >( insertValue ); // create root node
        else
            root.insert( insertValue ); // call the insert method
    } // end method insertNode

    // begin preorder traversal
    public void preorderTraversal()
    {
        preorderHelper( root );
    } // end method preorderTraversal

    // recursive method to perform preorder traversal
    private void preorderHelper( TreeNode< T > node )
    {
        if ( node == null )
            return;

        System.out.printf( "%s ", node.data ); // output node data
        preorderHelper( node.leftNode );     // traverse left subtree
        preorderHelper( node.rightNode );    // traverse right subtree
    } // end method preorderHelper

    // begin inorder traversal
    public void inorderTraversal()
    {
```

Fig. 22.17 | TreeNode and Tree class declarations for a binary search tree. (Part 1 of 3.)
