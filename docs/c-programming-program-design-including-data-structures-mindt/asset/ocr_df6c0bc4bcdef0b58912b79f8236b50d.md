```
```cpp
p->info = current->info;

if (trailCurrent == nullptr) //current did not move;
                             //current == p->pLink; adjust p
    p->lLink = current->lLink;
else
    trailCurrent->rLink = current->rLink;

delete current;
} //end else
} //end deletefromTree
```
```

Next, we describe the function deleteNode. The function deleteNode first searches the binary search tree to find the node containing the item to be deleted. The item to be deleted, deleteItem, is passed as a parameter to the function. If the node containing deleteItem is found in the binary search tree, the function deleteNode calls the function delete-fromTree to delete the node. The definition of the function deleteNode is given next.

```
```cpp
template <class elemType>
void BinarySearchTree<elemType>::deleteNode
                                      (const elemType deleteItem)
{
    nodeType<elemType> *current; //pointer to traverse the tree
    nodeType<elemType> *trailCurrent; // pointer behind current
    bool found = false;

    if (root == nullptr)
        cout << "Cannot delete from an empty tree."
             << endl;
    else
    {
        current = root;
        trailCurrent = root;

        while (current != nullptr && !found)
        {
            if (current->info == deleteItem)
                found = true;
            else
            {
                trailCurrent = current;
                if (current->info > deleteItem)
                    current = current->lLink;
                else
                    current = current->rLink;
            }
        } //end while

        if (current == nullptr)
            cout << "The item to be deleted is not in the tree."
                 << endl;
```
```