# Display 17.23 A Binary Tree

![](bbox=[0.11, 0.2, 0.92, 0.6])

Left subtree

Right subtree

```
class IntTreeNode
{
public:
    IntTreeNode(int theData, IntTreeNode* left, IntTreeNode* right)
        : data(theData), leftLink(left), rightLink(right){}
private:
    int data;
    IntTreeNode *leftLink;
    IntTreeNode *rightLink;
};

IntTreeNode *root;
```