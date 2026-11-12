```
template<class ItemType>
Node<ItemType>::Node() : next(nullptr)
{ // end default constructor

template<class ItemType>
Node<ItemType>::Node(const ItemType& anItem) : item(anItem), next(nullptr)
{ // end constructor

template<class ItemType>
Node<ItemType>::Node(const ItemType& anItem, Node<ItemType>* nextNodePtr) :
item(anItem), next(nextNodePtr)
{ // end constructor

template<class ItemType>
void Node<ItemType>::setItem(const ItemType& anItem)
{
item = anItem;
} // end setItem

template<class ItemType>
void Node<ItemType>::setNext(Node<ItemType>* nextNodePtr)
{
next = nextNodePtr;
} // end setNext

template<class ItemType>
ItemType Node<ItemType>::getItem() const
{
return item;
} // end getItem

template<class ItemType>
Node<ItemType>* Node<ItemType>::getNext() const
{
return next;
} // end getNext
```

# 4.2 A Link-Based Implementation of the ADT Bag

Now that we have a class of nodes to use when defining link-based data structures, we will use it to define a link-based implementation of the ADT Bag. Doing so will allow us to examine some of the basic practices for creating such implementations. Subsequent chapters will expand on these ideas.

Unlike array-based implementations, a link-based implementation does not impose a fixed maximum size on the data structure—except, of course, as imposed by the storage limits of the system. Additionally, data items do not move during an ADT's insertion and removal operations.

You need to represent the items in the ADT bag and its size. Figure 4-5 indicates one possible way to represent this data by using pointers. Here headPtr points to a linked chain of the nodes

![](bbox=[0.79, 0.73, 0.92, 0.8])