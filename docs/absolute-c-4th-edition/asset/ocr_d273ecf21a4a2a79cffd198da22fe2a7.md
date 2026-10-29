```
preorderShow(subTreeRoot->rightLink);
}
```

```
template<class T> //uses iostream:
void SearchTree<T>::postorderShow() const
{
    postorderShow(root);
}
```

```
template<class T> //uses iostream:
void SearchTree<T>::postorderShow(
    TreeNode<T>* subTreeRoot) const
{
    if (subTreeRoot != NULL)
    {
        postorderShow(subTreeRoot->leftLink);
        postorderShow(subTreeRoot->rightLink);
        cout << subTreeRoot->data << " ";
    }
}
```

# PROGRAMMING PROJECTS

+   1. Write a void function that takes a linked list of integers and reverses the order of its nodes. The function will have one call-by-reference parameter that is a pointer to the head of the list. After the function is called, this pointer will point to the head of a linked list that has the same nodes as the original list but in the reverse of the order they had in the original list. Note that your function will neither create nor destroy any nodes. It will simply rearrange nodes. Place your function in a suitable test program.

+   2. Write a function called mergeLists that takes two call-by-reference arguments that are pointer variables that point to the heads of linked lists of values of type int. The two linked lists are assumed to be sorted so that the number at the head is the smallest number, and so forth. The function returns a pointer to the head of a new linked list that contains all the nodes in the original two lists. The nodes in this longer list are also sorted from smallest to largest values. Note that your function will neither create nor destroy any nodes. When the function call ends, the two pointer variable arguments should have the value NULL.

+   3. Design and implement a class that is a class for polynomials. The polynomial aₙxⁿ + aₙ₋₁xⁿ⁻¹ + ... + a₀ will be implemented as a linked list. Each node will contain an int value for the power of x and an int value for the corresponding coefficient. The class operations should include addition, subtraction, multiplication, and evaluation of a polynomial. Overload the