```
```cpp
void dvdBinaryTree::searchDVDList(string title,
                                  bool& found,
                                  nodeType<dvdType>* &current) const
{
    found = false;

    dvdType temp;

    temp.setDVDInfo(title, "", "", "", "", 0);

    if (root == NULL)    //tree is empty
        cout << "Cannot search an empty list." << endl;
    else
    {
        current = root;  //set current point to the root node
                         //of the binary tree
        found = false;   //set found to false

        while (current != NULL && !found)  //search the tree
            if (current->info == temp)     //item is found
                found = true;
            else if (current->info > temp)
                current = current->lLink;
            else
                current = current->rLink;
    }   //end else
}   //end searchDVDList
```
```

Given a pointer to the root node of the binary tree containing the DVDs, the function `inorderTitle` uses the inorder traversal algorithm to print the titles of the DVDs. Notice that this function outputs only the DVD titles. The definition of this function is as follows:

```
```cpp
void dvdBinaryTree::inorderTitle
                      (nodeType<dvdType> *p) const
{
    if (p != NULL)
    {
        inorderTitle(p->lLink);
        p->info.printTitle();
        inorderTitle(p->rLink);
    }
}
```
```

The function `dvdPrintTitle` uses the function `inorderTitle` to print the titles of all DVDs in the store. The definition of this function is:

```
```cpp
void dvdBinaryTree::dvdPrintTitle() const
{
    inorderTitle(root);
}
```
```