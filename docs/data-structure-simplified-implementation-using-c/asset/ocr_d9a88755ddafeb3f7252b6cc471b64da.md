# Tree

![](bbox=[0.22, 0.12, 0.85, 0.42])

a) Original tree

b) Mirror tree

Figure 7-18: Mirroring of a tree

```
// function to find out the mirror of a BST
void bst::mirror ()
{
    bnode *current,*temp, *x=root;
    queue<bnode*> q1;
    q1.enqueue(x); // inserting the node into queue
    while (! q1.isEmpty ()) // Till queue is not empty
    {
    current=q1.dequeue ();        // take out one node from a queue
    temp=current->left;           // swap left and right node
    current->left=current->right;
    current->right=temp;
    if (current->left!=NULL)// if left is not NULL insert in queue
    q1.enqueue (current->left); //insert left node in a queue
    if(current->right!=NULL)    // if right is not NULL
    q1.enqueue(current->right); // insert right node in a queue
    }// end of while statement
}    // end of function
```