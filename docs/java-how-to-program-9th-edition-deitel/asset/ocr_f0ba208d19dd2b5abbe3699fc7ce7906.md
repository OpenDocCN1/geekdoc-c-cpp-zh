```
32      // insert in right subtree
33      else if ( insertValue.compareTo( data ) > 0 )
34      {
35          // insert new TreeNode
36          if ( rightNode == null )
37              rightNode = new TreeNode< T >( insertValue );
38          else // continue traversing right subtree recursively
39              rightNode.insert( insertValue );
40      } // end else if
41      } // end method insert
42  } // end class TreeNode
43
44  // class Tree definition
45  public class Tree< T extends Comparable< T > >
46  {
47      private TreeNode< T > root;
48
49      // constructor initializes an empty Tree of integers
50      public Tree()
51      {
52          root = null;
53      } // end Tree no-argument constructor
54
55      // insert a new node in the binary search tree
56      public void insertNode( T insertValue )
57      {
58          if ( root == null )
59              root = new TreeNode< T >( insertValue ); // create root node
60          else
61              root.insert( insertValue ); // call the insert method
62      } // end method insertNode
63
64      // begin preorder traversal
65      public void preorderTraversal()
66      {
67          preorderHelper( root );
68      } // end method preorderTraversal
69
70      // recursive method to perform preorder traversal
71      private void preorderHelper( TreeNode< T > node )
72      {
73          if ( node == null )
74              return;
75
76          System.out.printf( "%s ", node.data ); // output node data
77          preorderHelper( node.leftNode );     // traverse left subtree
78          preorderHelper( node.rightNode );    // traverse right subtree
79      } // end method preorderHelper
80
81      // begin inorder traversal
82      public void inorderTraversal()
83      {
```