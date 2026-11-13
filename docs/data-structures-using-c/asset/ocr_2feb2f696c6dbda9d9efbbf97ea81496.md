# 7.11.4 Preorder Traversal

These threads also simplify the algorithm for preorder and postorder traversals. Program Code 7.17 is the C++ routine for preorder traversal of a TBT.

```
PROGRAM CODE 7.17
// Traverse a threaded tree in preorder
void TBTree :: preorder()
{
    TBTNode *temp;
    int flag = 0;
    temp = Root;
    while(temp != head)
    {
        if(flag == 0) cout << temp->data << "*";
        if(temp->lbit == 1 && flag == 0) // go left till
            lbit is 1
        {
            temp = temp->left;
        }
        else if(temp->rbit == 1) // go to right by child
        {
            temp = temp->right;
            flag = 0;
        }
        else // go to right by thread
        {
            temp = temp->right;
            flag = 1;
        }
    } //End of function
```

# 7.11.5 Insert to Right of a Node

Consider Figs 7.72(a) and (b). We want to insert the node t to the right of the node s in both the threaded trees.