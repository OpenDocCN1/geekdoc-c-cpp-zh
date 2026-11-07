Let us think in terms of recursion. We cannot print the `info` of the first node until we have printed the remainder of the list (that is, the tail of the first node). Similarly, we cannot print the `info` of the second node until we have printed the tail of the second node, and so on. Every time we consider the tail of a node, we reduce the size of the list by 1. Eventually, the size of the list will be reduced to zero, in which case the recursion will stop. Let us first write the algorithm in pseudocode. (Suppose that `current` is a pointer to a linked list.)

```
```text
if (current != nullptr)
{
    reversePrint(current->link);   // print the tail
    cout << current->info << endl;  // print the node
}
```
```

Here, we do not see the base case; it is hidden. The list is printed only if the pointer to the list is not `nullptr`. Also, in the body of the `if` statement, the recursive call is on the tail of the list. Because eventually the tail of the list will be empty, the `if` statement in the next call will fail, and the recursion will stop. Also, note that no statements (for example, printing the `info` of the node) appear after the recursive call; thus, when the transfer comes back to the calling function, we must execute the remaining statements. Recall that the function exits only after the last statement executes. (By the “last statement,” we do not mean the physical last statement, but rather the logical last statement.)

Let us write the previous function in C++ and then apply it to a list.

```
```cpp
template <class Type>
void linkedListType<Type>::reversePrint
                         (nodeType<Type> *current) const
{
    if (current != nullptr)
    {
        reversePrint(current->link);   // print the tail
        cout << current->info << " ";  // print the node
    }
}
```
```

Consider the statement

```
```cpp
reversePrint(first);
```
```

in which `first` is a pointer of type `nodeType<Type>`.

Let us trace the execution of this statement, which is a function call, for the list shown in Figure 16-37. Because the formal parameter is a value parameter, the value of the actual parameter is passed to the formal parameter. See Figure 16-38.