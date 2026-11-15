```
//Constructors.
template<typename T>
Node<T>::Node() : data(0), left(0), right(0)
{
}
template<typename T>
Node<T>::Node(T v):data(v), left(0), right(0)
{
}
```

```
//Accessors
template<typename T>
node<T>* Node<T>::getLeft() const
{
    return left;
}
template<typename T>
Node<T>* Node<T>::getRight() const
{
    return right;
}
template<typename T>
T Node<T>::getData() const
{
    return data;
}
```

```
//Mutators
template<typename T>
void Node<T>::setLeft(Node<T>* l)
{
    left=l;
}
template<typename T>
void Node<T>::setRight(Node<T>* r)
{
    right=r;
}
template<typename T>
void Node<T>::setData(T v)
{
    data=v;
}
/**......................................................*/
```

Notice that the class implementation requires that each method be defined as a method template.

The class template definition for BinaryTree follows:

```
/**......................................................*/
/* Binary tree declaration                             */
/* filename: binaryTreeTemplate.h                      */
```