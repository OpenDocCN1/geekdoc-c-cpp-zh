
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

## 快速复习

- 1. 二叉树要么为空，要么有一个称为根节点的特殊节点。如果树非空，则根节点有两组节点，分别称为左子树和右子树，并且左子树和右子树也都是二叉树。
- 2. 二叉树的节点中有两个链接。
- 3. 二叉树中没有左孩子和右孩子的节点称为叶节点。
- 4. 如果从 U 到 V 有一条分支，则节点 U 称为节点 V 的父节点。
- 5. 二叉树中从节点 X 到节点 Y 的路径是一个节点序列 X<sub>0</sub>, X<sub>1</sub>, ..., X<sub>n</sub>，满足 (a) X = X<sub>0</sub>，X<sub>n</sub> = Y，且 (b) 对所有 i = 1, 2, ..., n，X<sub>i−1</sub> 是 X<sub>i</sub> 的父节点。也就是说，存在从 X<sub>0</sub> 到 X<sub>1</sub>、从 X<sub>1</sub> 到 X<sub>2</sub>、...、从 X<sub>i−1</sub> 到 X<sub>i</sub>、...、从 X<sub>n−1</sub> 到 X<sub>n</sub> 的分支。
- 6. 二叉树中路径的长度是该路径上的分支数。
- 7. 二叉树中节点的层次是从根到该节点的路径上的分支数。
- 8. 二叉树根节点的层次为 0，根节点的孩子的层次为 1。
- 9. 二叉树的高度是从根到叶子的最长路径上的节点数。
- 10. 在中序遍历中，二叉树的遍历方式如下：
  - a. 遍历左子树。
  - b. 访问该节点。
  - c. 遍历右子树。
- 11. 在前序遍历中，二叉树的遍历方式如下：
  - a. 访问该节点。
  - b. 遍历左子树。
  - c. 遍历右子树。
- 12. 在后序遍历中，二叉树的遍历方式如下：
  - a. 遍历左子树。
  - b. 遍历右子树。
  - c. 访问该节点。
- 13. 二叉搜索树 T 要么为空，要么：
  - i. T 有一个称为根节点的特殊节点；
  - ii. T 有两组节点 L<sub>T</sub> 和 R<sub>T</sub>，分别称为 T 的左子树和右子树；
  - iii. 根节点中的关键字大于左子树中的每个关键字，并且小于右子树中的每个关键字；且
  - iv. L<sub>T</sub> 和 R<sub>T</sub> 都是二叉搜索树。
- 14. 要从一棵左子树和右子树都非空的二叉搜索树中删除一个节点，首先定位其直接前驱，然后将前驱的信息复制到该节点中，最后删除该前驱。

## 练习

每道练习末尾括号中的数字指本章开头列出的学习目标。

- 1. 判断以下陈述是否正确。
  - a. 二叉树必须非空。(1, 2)
  - b. 根节点的层次为 0。(1, 2)
  - c. 如果一棵树只有一个节点，则树的高度为 0，因为层数为 0。(2)
  - d. 二叉树中节点的层次是从根到该节点的路径上的分支数。(2)
  - e. 二叉树的中序遍历总是按升序输出数据。(3)
  - f. 在二叉树的前序遍历中，先访问该节点，再访问左子树和右子树。(3)
  - g. 在二叉搜索树中，节点中的数据大于其左孩子（如果有）中的数据。(5)
  - h. 在二叉搜索树中，节点的左子树和右子树都是二叉搜索树。(5)
  - i. 要在二叉搜索树中插入一个新项，首先搜索该二叉搜索树，找到要插入新项的位置。(7)
  - j. 通常，使用栈来实现二叉树的非递归遍历算法。(8)
  - k. 在 C++ 中，不带任何括号的函数名被视为指向该函数的指针。(9)
- 2. 有 14 棵具有四个节点的不同二叉树。画出所有这些二叉树。(1, 2)

图 19-13 中的二叉树将用于练习 3 到 20。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1450_0.png)

图 19-14 练习 21 至 25 用图

- 21. 列出从信息为 68 的节点到信息为 90 的节点的路径。(2, 5)
- 22. 将信息为 58 的节点插入树中。列出 insert 函数为插入 58 所访问的节点。画出插入 58 后的树。(7)
- 23. 删除节点 60 并重画二叉树。(7)
- 24. 按此顺序删除节点 50 和 95。每次删除后重画二叉树。(7)
- 25. 删除节点 75 并重画二叉树。(7)
- 26. 将 28、25、26、42、47、30、45、29、5 插入一棵初始为空的二叉搜索树。画出最终的二叉搜索树。(6, 7)
- 27. 证明一棵有 n 个节点的二叉树恰好有 n + 1 个空子树（nullptr）。(1, 2)
- 28. 假设给定与中序序列和前序序列相对应的两个元素序列。证明可以重构出唯一的二叉树。(1, 3)
- 29. 下面按两种不同顺序列出二叉树中的节点：
  前序：ABCDEFGHIJKLM
  中序：CEDFBAHJIKGML
  画出该二叉树。(1, 3)

