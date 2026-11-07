![](bbox=[0.199, 0.122, 0.897, 0.224])

FIGURE 18-33  middle after traversing the list

It is now easy to divide the list into two sublists. First, using the link of **middle**, we assign a pointer to the node following **middle**. Then, we set the link of **middle** to **nullptr**. Figure 18--34 shows the resulting sublists.

![](bbox=[0.199, 0.353, 0.897, 0.508])

FIGURE 18-34  List after dividing it into two lists

This discussion translates into the following C++ function, **divideList**:

```
template <class Type>
void unorderedLinkedList<Type>::
                 divideList(nodeType<Type>* first1,
                             nodeType<Type>* &first2)
{
    nodeType<Type>* middle;
    nodeType<Type>* current;

    if (first1 == nullptr)    //list is empty
        first2 = nullptr;
    else if (first1->link == nullptr)  //list has only one node
        first2 = nullptr;
    else
    {
        middle = first1;
        current = first1->link;

        if (current != nullptr)       //list has more than two nodes
            current = current->link;
        while (current != nullptr)
```