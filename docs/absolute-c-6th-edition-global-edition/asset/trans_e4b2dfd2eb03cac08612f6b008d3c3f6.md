

# 二叉搜索树存储规则

+   1. 左子树中的所有值都小于根节点中的值。
+   2. 右子树中的所有值都大于或等于根节点中的值。
+   3. 该规则递归地适用于两个子树中的每一个。
+   
+   （递归的基本情况是一个空树，它始终被认为满足该规则。）

请注意，如果一棵树满足二叉搜索树存储规则，并且你使用中序处理方法输出值，则数字将按从小到大的顺序输出。

对于遵循二叉搜索树存储规则且呈矮胖而非细长的树，可以使用与 Display 13.5 中介绍的二分搜索算法精神相似的二分搜索算法从树中非常快速地检索值。搜索和维护二叉存储树以实现这种效率的主题是一个很大的主题，超出了我们在此可容纳的范围。

## 示例：一个树模板类

Display 17.36 包含二叉搜索树的模板类定义。在此示例中，我们将 SearchTree 类设为 TreeNode 类的友元类。这使我们能够在树类成员变量的定义中按名称访问节点成员变量。该 SearchTree 类的实现在 Display 17.37 中给出，演示程序在 Display 17.38 中给出。

该模板类旨在让你体会树处理的精髓，但它并不是一个完整的示例。真正的类会有更多的成员函数。特别是，真正的树类会有拷贝构造函数和重载的赋值运算符。我们省略了这些以节省空间。

关于类 SearchTree 中函数定义的某些内容需要观察。函数 insert 和 inTree 是重载的。单参数版本是我们需要的。然而，最清晰的算法是递归的，而递归算法需要一个额外的参数作为子树的根。因此，我们为这些函数中的每一个定义了带两个参数的私有辅助函数，并在双参数函数中实现了递归算法。然后单参数函数只需调用双参数版本，并将子树根参数设置为整个树的根。对于重载的 delete 函数名 inorderShow 也是类似的情况。函数 deleteSubtree 对析构函数起着类似的作用。

## Display 17.36 树模板类的接口文件

```
//Header file tree.h. The only way to insert data in a tree is with the
//insert function. So, the tree satisifies the Binary Search Tree Storage
//Rule. The function intree depends on this. < must be defined and
//give a well-behaved ordering on the type T.
#ifndef TREE_H
#define TREE_H
namespace TreeSavitch
{
    template<class T>
    class TreeNode; //forward declaration

    template<class T>
    class TreeNode
    {
    public:
        TreeNode( ) : root(nullptr){
            TreeNode<T>* left, TreeNode<T>* right,
                : data(theData), leftLink(left), rightLink(right){
            friend class SearchTree<T>;
    private:
        T data;
        TreeNode<T> *leftLink;
        TreeNode<T> *rightLink;
    };

    template<class T>
    class SearchTree
    {
    public:
        SearchTree( ) : root(nullptr){
        virtual ~SearchTree( );
        void insert(T item);//Adds item to the tree.
        bool inTree(T item) const;
        void inorderShow( ) const;
    private:
        void insert(T item, TreeNode<T>*& subTreeRoot);
        bool inTree(T item, TreeNode<T>* subTreeRoot) const;
        void deleteSubtree(TreeNode<T>*& subTreeRoot);
        void inorderShow(TreeNode<T>* subTreeRoot) const;
        TreeNode<T>* root;
    };
}//TreeSavitch

#endif
```

> SearchTree 模板类应具有拷贝构造函数、赋值运算符的重载以及其他成员函数。然而，我们再次省略了这些函数以保持此示例简短。真正的模板类将包含更多成员函数和重载运算符。

## Display 17.37 树模板类的实现文件（第 1 部分，共 2 部分）

//This is the implementation file tree.cpp. This is the implementation
//for the template class SearchTree. The interface is in the file tree.h.
namespace TreeSavitch
{
    template<class T>
    void SearchTree<T>::insert(T item, TreeNode<T>*& subTreeRoot)
    {
        if (subTreeRoot == nullptr)
            subTreeRoot = new TreeNode<T>(item, nullptr, nullptr);
        else if (item < subTreeRoot->data)
            insert(item, subTreeRoot->leftLink);
        else//item >= subTreeRoot->data
            insert(item, subTreeRoot->rightLink);
    }

    template<class T>
    void SearchTree<T>::insert(T item)
    {
        insert(item, root);
    }

    template<class T>
    bool SearchTree<T>::inTree(T item, TreeNode<T>* subTreeRoot) const
    {
        if (subTreeRoot == nullptr)
            return false;
        else if (subTreeRoot->data == item)
            return true;
        else if (item < subTreeRoot->data)
            return inTree(item, subTreeRoot->leftLink);
        else//item >= link->data
            return inTree(item, subTreeRoot->rightLink);
    }

    template<class T>
    bool SearchTree<T>::inTree(T item) const
    {
        return inTree(item, root);
    }
}

如果所有数据都使用函数 insert 输入，则树将满足二叉搜索树存储规则。

函数 in Tree 使用了一种二分搜索算法，它是 Display 13.5 中给出的算法的变体。

## Display 17.37 树模板类的实现文件（第 2 部分，共 2 部分）

```
36 }
37 template<class T>//uses iostream:
38 void SearchTree<T>::inorderShow(TreeNode<T>* subTreeRoot) const
39 {
40     if (subTreeRoot != nullptr)
41     {
42         inorderShow(subTreeRoot->leftLink);
43         cout << subTreeRoot->data << " ";
44         inorderShow(subTreeRoot->rightLink);
45     }
46 }
47 
48 template<class T>//uses iostream:
49 void SearchTree<T>::inorderShow() const
50 {
51     inorderShow(root);
52 }
53 
54 template<class T>
55 void SearchTree<T>::deleteSubtree(TreeNode<T>*& subTreeRoot)
56 {
57     if (subTreeRoot != nullptr)
58     {
59         deleteSubtree(subTreeRoot->leftLink);
60         deleteSubtree(subTreeRoot->rightLink);
61         //subTreeRoot now points to a one node tree.
62         delete subTreeRoot;
63         subTreeRoot = nullptr;
64     }
65 }
66 
67 template<class T>
68 SearchTree<T>::~SearchTree()
69 {
70     deleteSubtree(root);
71 }
72 }//TreeSavitch

Uses in-order traversal of the tree
Uses postorder traversal of the tree
```

- *双向链表* 中的节点有两个链接——一个指向列表中前一个节点的链接，一个指向下一个节点的链接。这使得插入和删除等操作变得稍微容易一些。
- *栈* 是一种后进先出的数据结构。*队列* 是一种先进先出的数据结构。两者都可以使用链表实现。
- *哈希表* 是一种用于存储对象并高效检索它们的数据结构。*哈希函数* 用于将对象映射到一个值，然后该值可用于索引该对象。
- 链表可用于实现集合，包括并集、交集和集合成员资格等常见操作。
- *迭代器* 是一种构造（通常是某个迭代器类的对象），它允许你遍历存储在数据结构中的数据项。
- *树* 是一种数据结构，其节点有两个（或更多）指向其他节点的成员变量的指针。如果一棵树满足 *二叉搜索树存储规则*，则可以设计一个函数来快速在树中找到数据。

## 自测练习答案

- 1. Sally
  Sally
  18
  请注意，(*head).name 和 head->name 含义相同。同样，(*head).number 和 head->number 含义相同。
- 2. 最佳答案是
  head->next = nullptr;
  然而，以下也是正确的：
  (*head).next = nullptr;
- 3. head->item = "Wilbur's brother Orville";
- 4. class NodeType
  {
  public:
  NodeType() {}
  NodeType(char theData, NodeType* theLink)
  : data(theData), link(theLink) {}
  NodeType* getLink() const { return link; }

