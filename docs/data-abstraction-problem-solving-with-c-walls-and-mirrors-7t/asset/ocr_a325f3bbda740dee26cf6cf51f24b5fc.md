Let's write some high-level pseudocode for this loop, given the linked chain pictured in Figure 4-5.

```
Let a current pointer point to the first node in the chain
while (the current pointer is not the null pointer)
    Assign the data portion of the current node to the next element in a vector
    Set the current pointer to the next pointer of the current node
}
```

This solution requires that you keep track of the current position within the chain. Thus, you need a pointer variable—let's call it curPtr—that points to the current node.

Note: The pointer variable curPtr is analogous to the integer variable curIndex that we used in Section 3.2.4 of Chapter 3 to keep track of the current entry in an array.

Initially, curPtr must point to the first node. Because headPtr points to the first node, simply copy headPtr into curPtr by writing Node<ItemType>* curPtr = headPtr;

Then you can use the expression curPtr->getItem() to access the data portion of the current node. After copying the data into the vector, you advance the current pointer to the next node by writing curPtr = curPtr->getNext();

Figure 4-7 illustrates this action. If the previous assignment statement is not clear, consider Node<ItemType>* temp = curPtr->getNext(); curPtr = temp;

and then convince yourself that the intermediate variable temp is not necessary.

# FIGURE 4-7 The effect of the assignment curPtr = curPtr->getNext()

![](bbox=[0.07, 0.62, 0.77, 0.76])

These ideas lead to the following definition of toVector:

```
template<class ItemType>
vector<ItemType> LinkedBag<ItemType>::toVector() const
{
vector<ItemType> bagContents;
Node<ItemType>* curPtr = headPtr;
int counter = 0;
while ((curPtr != nullptr) && (counter < itemCount))
```