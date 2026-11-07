
```cpp
{
    switch (choice)
    {
    case 1:
        cout << "Enter the title: ";
        getline(cin, title);
        cout << endl;

        if (dvdList.dvdSearch(title))
            cout << "The store carries " << title << endl;
        else
            cout << "The store does not carry " << title
                 << endl;
        break;

    case 2:
        cout << "Enter the title: ";
        getline(cin, title);
        cout << endl;

        if (dvdList.dvdSearch(title))
        {
            if (dvdList.isDVDAvailable(title))
            {
                dvdList.dvdCheckOut(title);
                cout << "Enjoy your movie: " << title
                     << endl;
            }
            else
                cout << "Currently " << title
                     << " is out of stock." << endl;
        }
        else
            cout << "The store does not carry " << title
                 << endl;
        break;

    case 3:
        cout << "Enter the title: ";
        getline(cin, title);
        cout << endl;

        if (dvdList.dvdSearch(title))
        {
            dvdList.dvdCheckIn(title);
            cout << "Thanks for returning " << title
                 << endl;
        }
        else
            cout << "The store does not carry " << title
                 << endl;
        break;

    case 4:
        cout << "Enter the title: ";
        getline(cin, title);
        cout << endl;

        if (dvdList.dvdSearch(title))
        {
            if (dvdList.isDVDAvailable(title))
                cout << title << " is currently in "
                     << "stock." << endl;
            else
                cout << title << " is currently out "
                     << "of stock." << endl;
        }
        else
            cout << "The store does not carry " << title
                 << endl;
        break;

    case 5:
        dvdList.dvdPrintTitle();
        break;

    case 6:
        dvdList.inorderTraversal();
        break;

    default:
        cout << "Invalid selection." << endl;
    } //end switch

    displayMenu();              //display the menu
    cout << "Enter your choice: ";
    cin >> choice;               //get the next request
    cin.ignore(100, '\n');       //ignore the remaining
                                 //characters in the line
    cout << endl;
} //end while

return 0;
}

void createDVDList(ifstream& infile,
                   dvdBinaryTree<dvdType>& dvdList)
{
    string title;
    string star1;
    string star2;
    string producer;
    string director;
    string productionCo;
    int inStock;

    dvdType newDVD;

    getline(infile, title);

    while (infile)
    {
        getline(infile, star1);
        getline(infile, star2);
        getline(infile, producer);
        getline(infile, director);
        getline(infile, productionCo);
        infile >> inStock;
        infile.ignore(100, '\n');
        newDVD.setDVDInfo(title, star1, star2, producer,
                          director, productionCo, inStock);
        dvdList.insert(newDVD);

        getline(infile, title);
    } //end while
} //end createDVDList

void displayMenu()
{
    cout << "Select one of the following:" << endl;
    cout << "1: To check whether the store carries a "
         << "particular DVD." << endl;
    cout << "2: To check out a DVD." << endl;
    cout << "3: To check in a DVD." << endl;
    cout << "4: To check whether a particular DVD is "
         << "in stock." << endl;
    cout << "5: To print only the titles of all the DVDs."
         << endl;
    cout << "6: To print a list of all the DVDs." << endl;
    cout << "9: To exit" << endl;
}
```

## QUICK REVIEW

- 1. A binary tree is either empty or it has a special node called the root node. If the tree is nonempty, the root node has two sets of nodes, called the left and right subtrees, such that the left and right subtrees are also binary trees.
- 2. The node of a binary tree has two links in it.
- 3. A node in the binary tree is called a leaf if it has no left and right children.
- 4. A node U is called the parent of a node V if there is a branch from U to V.
- 5. A path from a node X to a node Y in a binary tree is a sequence of nodes X<sub>0</sub>, X<sub>1</sub>, ..., X<sub>n</sub> such that (a) X = X<sub>0</sub>, X<sub>n</sub> = Y, and (b) X<sub>i−1</sub> is the parent of X<sub>i</sub> for all i = 1, 2, ..., n. That is, there is a branch from X<sub>0</sub> to X<sub>1</sub>, X<sub>1</sub> to X<sub>2</sub>, ..., X<sub>i−1</sub> to X<sub>i</sub>, ..., X<sub>n−1</sub> to X<sub>n</sub>.
- 6. The length of a path in a binary tree is the number of branches on that path.
- 7. The level of a node in a binary tree is the number of branches on the path from the root to the node.
- 8. The level of the root node of a binary tree is 0, and the level of the children of the root node is 1.
- 9. The height of a binary tree is the number of nodes on the longest path from the root to a leaf.
- 10. In an inorder traversal, the binary tree is traversed as follows:
  - a. Traverse the left subtree.
  - b. Visit the node.
  - c. Traverse the right subtree.
- 11. In a preorder traversal, the binary tree is traversed as follows:
  - a. Visit the node.
  - b. Traverse the left subtree.
  - c. Traverse the right subtree.
- 12. In a postorder traversal, the binary tree is traversed as follows:
  - a. Traverse the left subtree.
  - b. Traverse the right subtree.
  - c. Visit the node.
- 13. A binary search tree T is either empty or:
  - i. T has a special node called the root node;
  - ii. T has two sets of nodes, L<sub>T</sub> and R<sub>T</sub>, called the left subtree and the right subtree of T, respectively;
  - iii. The key in the root node is larger than every key in the left subtree and smaller than every key in the right subtree; and
  - iv. L<sub>T</sub> and R<sub>T</sub> are binary search trees.
- 14. To delete a node from a binary search tree that has both left and right nonempty subtrees, first its immediate predecessor is located, then the predecessor’s info is copied into the node, and finally the predecessor is deleted.

## EXERCISES

The number in parentheses at the end of an exercise refers to the learning objective listed at the beginning of the chapter.

- 1. Mark the following statements as true or false.
  - a. A binary tree must be nonempty. (1, 2)
  - b. The level of the root node is 0. (1, 2)
  - c. If a tree has only one node, the height of the tree is 0 because the number of levels is 0. (2)
  - d. The level of a node in a binary tree is the number of branches on the path from the root to the node. (2)
  - e. The inorder traversal of a binary tree always outputs the data in ascending order. (3)
  - f. In preorder traversal of a binary tree, the node is visited before visiting the left and right subtrees. (3)
  - g. In a binary search tree, the data in a node is larger than the data in its left child, if any. (5)
  - h. In a binary search tree, the left and right subtrees of a node are binary search trees. (5)
  - i. To insert a new item in a binary search tree, first we search the binary search tree and find the place where the new item is to be inserted. (7)
  - j. Typically, a stack is used to implement a nonrecursive traversal algorithm in a binary tree. (8)
  - k. In C++, a function name without any parentheses is considered a pointer to the function. (9)
- 2. There are 14 different binary trees with four nodes. Draw all of them. (1, 2)

The binary tree of Figure 19-13 is to be used for Exercises 3 through 20.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1450_0.png)

FIGURE 19-14 Figure for Exercises 21 to 25

- 21. List the path from the node with info 68 to the node with info 90. (2, 5)
- 22. A node with info 58 is to be inserted in the tree. List the nodes that are visited by the function insert to insert 58. Redraw the tree after inserting 58. (7)
- 23. Delete node 60 and redraw the binary tree. (7)
- 24. Delete nodes 50 and 95 in that order. Redraw the binary tree after each deletion. (7)
- 25. Delete node 75 and redraw the binary tree. (7)
- 26. Insert 28, 25, 26, 42, 47, 30, 45, 29, 5 into an initially empty binary search tree. Draw the final binary search tree. (6, 7)
- 27. Prove that a binary tree with n nodes has exactly n + 1 empty subtree (nullptr). (1, 2)
- 28. Suppose that you are given two sequences of elements corresponding to the inorder sequence and the preorder sequence. Prove that it is possible to reconstruct a unique binary tree. (1, 3)
- 29. The following lists the nodes in a binary tree in two different orders:
  preorder: ABCDEFGHIJKLM
  inorder: CEDFBAHJIKGML
  Draw the binary tree. (1, 3)
