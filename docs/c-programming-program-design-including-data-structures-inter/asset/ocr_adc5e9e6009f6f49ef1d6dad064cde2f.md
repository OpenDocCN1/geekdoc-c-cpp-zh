Figure 16-19 shows the UML class diagram of the class `linkedListIterator`.

![](bbox=[0.216, 0.154, 0.929, 0.334])

**FIGURE 16-19** UML class diagram of the class `linkedListIterator`

The definitions of the functions of the class `linkedListIterator` are:

```
template <class Type>
linkedListIterator<Type>::linkedListIterator()
{
    current = NULL;
}

template <class Type>
linkedListIterator<Type>::
                 linkedListIterator(nodeType<Type> *ptr)
{
    current = ptr;
}

template <class Type>
Type linkedListIterator<Type>::operator*()
{
    return current->info;
}

template <class Type>
linkedListIterator<Type> linkedListIterator<Type>::operator++()
{
    current = current->link;

    return *this;
}

template <class Type>
bool linkedListIterator<Type>::operator==
                 (const linkedListIterator<Type>& right) const
{
    return (current == right.current);
}
```