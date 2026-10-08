# 19.7 Trees 839

```
103
104  // recursive method to perform inorder traversal
105  private void InorderHelper(TreeNode node)
106  {
107      if (node != null)
108      {
109          // traverse left subtree
110          InorderHelper(node.LeftNode);
111      }
112
113      // output node data
114      Console.Write($"{node.Data}");
115
116      // traverse right subtree
117          InorderHelper(node.RightNode);
118      }
119  }
120
121  // begin postorder traversal
122  public void PostorderTraversal()
123  {
124      PostorderHelper(root);
125  }
126
127  // recursive method to perform postorder traversal
128  private void PostorderHelper(TreeNode node)
129  {
130      if (node != null)
131      {
132          // traverse left subtree
133          PostorderHelper(node.LeftNode);
134      }
135      // traverse right subtree
136          PostorderHelper(node.RightNode);
137      }
138
139      // output node Data
140      Console.Write($"{node.Data}");
141  }
142  }
```

Fig. 19.20 | Declaration of class TreeNode and class Tree. (Part 3 of 3)

```
1 // Fig. 19.21: TreeTest.cs
2 // Testing Tree class with a binary tree.
3 using System;
4 using BinaryTreeLibrary;
5
6 // class TreeTest declaration
7 class TreeTest
8 {
```

Fig. 19.21 | Testing class Tree with a binary tree. (Part 1 of 2.)