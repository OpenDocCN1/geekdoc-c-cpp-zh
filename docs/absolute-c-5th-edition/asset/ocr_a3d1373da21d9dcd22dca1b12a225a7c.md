# CHAPTER 17 Linked Data Structures

Display 17.36 Interface File for a Template Class

```
//Header file tree.h. The only way to insert data in a tree is with the
//insert function. So, the tree satisfies the Binary Search Tree Storage
//Rule. The function inTree depends on this. < must be defined and
//give a well-behaved ordering to the type T.
#ifndef TREE_H
#define TREE_H
namespace TreeSavitch
{
    template<class T>
    class SearchTree;//forward declaration

    template<class T>
    class TreeNode
    {
public:
        TreeNode() : root (NULL)
        TreeNode(T data, TreeNode<T>* left, TreeNode<T>* right)
            : data(data), leftLink(left), rightLink(right) {}
        friend class SearchTree;
    private:
        T data;
        TreeNode<T> *leftLink;
        TreeNode<T> *rightLink;
    };

    template<class T>
    class SearchTree
    {
public:
        SearchTree() : root (NULL)
        virtual ~SearchTree();
        void insert(T item) //Adds item to the tree.
        bool inTree(T item) const;
        void inorderShow() const;
    private:
        void insert(T item, TreeNode<T>* subRoot);
        bool inTree(T item, TreeNode<T>* subRoot) const;
        void deleteSubtree(TreeNode<T>* subRoot);
        void inorderShow(TreeNode<T>* subRoot) const;
        TreeNode<T>* root;
// The SearchTree template class should have a copy,
constructor, or an overloading of the assignment operator,
and other member functions. However, we have omitted
these functions to keep this example short. A real template
class would contain more member functions and overloaded
operators.
    };
//Treesavitch
#endif
```