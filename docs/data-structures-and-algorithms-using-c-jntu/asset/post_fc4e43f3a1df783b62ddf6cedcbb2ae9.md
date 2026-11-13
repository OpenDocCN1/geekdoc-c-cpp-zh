
```cpp
cout<<"\\nAVLTREE Operations\\n1.Insert\\n2.Delete\\n3.Traverse\\n";
cout<<"4.Height Of Tree\\n5.Searching\\n6.Exit";
cout<<"\\n\\nEnter Your Option";
cin>>n;
switch(n)
{
 case 1:insert();break;
 case 2:
 if(root==NULL) {cout<<"Tree Is Empty";break;}
 cout<<"\\n1.Delete Leaf Node\\n2.Delete Single Child Node";
 cout<<"\\n\\nEnter Your Option";
 cin>>op;
 switch(op)
 {
 case 1:deleleaf();break;
 case 2:delone();break;
 case 3:goto x;
 default:cout<<"Invalid Choice";
 }
 break;
 case 3:cout<<"Tree Elements Are:";inorder(root);break;
 case 4:height=findheight(root);
 cout<<"Height Of The Tree:"<<height;break;
 case 5:if(root==NULL) {cout<<"Tree Is Empty";break;}
 s=k=0;cout<<"Which Item You Want To Search";
 cin>>item;
 s=searching(root,item);
 if(s==1)
 cout<<"Item"<<item<<"Is Found";
 else
 cout<<"Item"<<item<<"Is Not Found";
 break;
 case 6:exit(0);
 default:cout<<"Invalid Choice";
 }
}
}
```

## Output

- AVLTREE Operations
- 1. Insert
- 2. Delete
- 3. Traverse
- 4. Height Of Tree
- 5. Searching
- 6. Exit

```
Enter Your Option 1
Enter Item To Be Insert 35
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 20
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 40
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 10
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 22
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 37
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 15
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 25
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 36
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 3
Tree Elements Are:10 15 20 22 25 35 36 37 40
1.Delete Leaf Node
2.Delete Single Child Node
Enter Your Option 1
Which Item You Want To Delete 15
Element Is Successfully deleted
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 3
Tree Elements Are:10 20 22 25 35 36 37 40
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 2
1.Delete Leaf Node
2.Delete Single Child Node
Enter Your Option 2
Which Item You Want To Delete 22
Element Is Successfully deleted
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 3
Tree Elements Are:10 20 25 35 36 37 40
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 4
Height Of The Tree:3
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 5
Which Item You Want To Search 37
Item 37 Is Found
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 6
```

## 12.6 APPLICATIONS

A self-balancing binary search tree has numerous applications. Its basic characteristic is to maintain the elements in order. So, it is applied in all the environment where the order of elements is required:

- 1. Priority queues
- 2. Associative array based on the order of elements the key-value pairs are inserted
- 3. Binary tree sort
- 4. Many algorithms in computational geometry such as line segment, intersection problem and point location problem
- 5. Internet routers

## SUMMARY

- • A non-empty binary search tree should satisfy the following properties:
  - 1. All the elements must have a key and it must be distinct.
  - 2. All the keys (if any) in the left subtree of the tree.
  - 3. All the keys (if any) in the right subtree of the tree must be greater than the root element.
  - 4. The left and right subtrees of the tree must also be the binary search trees.
- • The inorder traversal of a binary search tree produces the sorted list of the given elements in ascending order.
- • The operations on binary search tree are searching, insertion and deletion.
- • BST is highly efficient in performing all the operations with a time complexity of O(log n) over a sequential list.
- • Binary search trees suffers from the drawback of becoming skewed.
- • An empty binary tree is an AVL tree. A non-empty binary tree T is an AVL tree if and only if
  - 1. the left subtree TL and the right subtree TR of T are also AVL trees and
  - 2. |h(TL) - h(TR)| <= 1 where h(TL) and h(TR) are the heights of left and right subtrees of T, respectively.
- • The balancing factor of node u, bf(u) can be defined as bf(u)=h(UL)-h(UR), where, h(UL) is the height of the left subtree of u and h(UR) is the height of the right subtree of u.
- • Representation of AVL tree and AVL search trees are very similar to that of binary trees and binary search trees using a linked representation.
- • Searching, insertion and deletion are the common operations on AVL trees.
- • The insertion operation on AVL trees is similar to BST but leads to imbalance. The rotations LL, LR, RL, RR are used to rebalance the tree.
- • A deletion operation on AVL trees also performs some rotations.

## EXERCISES

### FILL IN THE BLANKS

- 1. The path from the root to an external node is known as an _______.
- 2. Linked representation of a binary search tree with a collection of internal nodes that represent the keys and external nodes that represent null pointers is known as _______.
- 3. The skewed binary search trees have the time complexity of _______.
- 4. Major classification of rotations while performing deletion in AVL trees is _______.
- 5. _______ are the rotations performed while inserting an element into an AVL tree.

### MULTIPLE-CHOICE QUESTIONS

- 1. _______ the time complexity in an average case where frequent insertions and/or deletions are assumed.
  - a. O(log n)
  - b. O(n)
  - c. O(n log n)
  - d. None

- 2. Which of the following traversal technique lists the nodes of a binary tree in ascending order?
  - a. Postorder
  - b. Inorder
  - c. Preorder
  - d. None

- 3. Consider this binary search tree:

![](img/45784b9f0334626143002ec0d63692fd_419_0.png)

- Suppose we remove the root, replacing it with something from the left subtree, what will be the new root?
  - a. 1
  - b. 2
  - c. 4
  - d. 5
  - e. 16

- 4. The balancing factor of a node u, bf(u) can be defined as _______.
  - a. bf(u_l)-h(u_r)
  - b. bf(u)-h(u_l)-h(u_r)
  - c. bf(u_l)+h(u_l)-h(u_r)
  - d. bf(u_l)+h(u_l)-h(u_r)

- 5. Which of the following statement is true?
  - a. An AVL search tree may require one rotation to rebalance it after deletion.
  - b. An AVL search tree may require more than one rotation, insertion requires single rotation.
  - c. An AVL search tree may require more than one rotation to rebalance it after deletion
  - d. None.

### SHORT-ANSWER QUESTIONS

- 1. Define binary search trees.
- 2. Define AVL trees.
- 3. Suppose that we want to create a binary search tree where each node contains information on some data type called Item (which has a default constructor and a correct value semantics), what additional factor is required for the Item data type?
- 4. Suppose that a binary search tree contains the number 42 as a node with two children. Write two or three clear sentences to describe the process required to delete 42 from the tree.
- 5. Consider the following AVL tree:

![](img/45784b9f0334626143002ec0d63692fd_420_0.png)

Show the modified tree under each of the following operations:
Deletion of the key 4
Insertion of the key 16.

### ESSAY QUESTIONS

- 1. Explain about binary search trees and its operations in detail.
- 2. Discuss in detail about AVL trees.
- 3. Give the representations of various rotations involved while inserting an element into an AVL tree.
- 4. Write an algorithm for performing deletion in AVL trees.
- 5. Explain various rotations involved while deleting an element from an AVL tree.
