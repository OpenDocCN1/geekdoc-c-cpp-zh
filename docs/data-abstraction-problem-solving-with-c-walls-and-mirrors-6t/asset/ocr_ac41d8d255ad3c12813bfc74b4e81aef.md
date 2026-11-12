```
// Link new node to end of new chain
newChainPtr->setNext(newNodePtr);

// Advance pointer to new last node
newChainPtr = newChainPtr->getNext();
} // end while

newChainPtr->setNext(nullptr); // Flag end of new chain
} // end if
} // end copy constructor
```

As you can see, the copy constructor is an expensive operation. It requires traversing the original linked chain and duplicating each node visited.

# 4.3 Using Recursion in Link-Based Implementations

It is possible, and sometimes desirable, to process linked chains recursively. This section examines how to write the iterative methods given previously as recursive ones. Such recursive methods will require the chain’s head pointer as an argument. Therefore, they should not be public, because the head pointer is a private data member of the class and the client does not—and should not—have access to it. Otherwise, clients could access the linked nodes directly, thereby violating the ADT’s wall.

# 4.3.1 Recursive Definitions of Methods in LinkedBag

As an introduction to this topic, we will revise two methods in the class LinkedBag to use recursion. These methods simply traverse a chain of linked nodes without making any changes to it.

**The method toVector.** We begin with the method toVector because it has a straightforward recursive implementation. This operation requires us to traverse the linked chain of nodes as we copy data from the nodes into a vector. Traversal of a linked chain is an operation that occurs in many situations.

We have established that the method performing the recursion must be private and must have the head pointer as a parameter. Since the method will copy data into a vector as it traverses the linked chain, the vector must also be a parameter. We can declare this method in the private section of the class LinkedBag, as follows:

```
// Fills the vector bagContents with the data in the nodes of
// the linked chain to which curPtr points.
void fillVector(vector<ItemType>& bagContents, Node<ItemType>* curPtr) const
```

Given a definition of this method, we could implement toVector as follows:

```
template<class ItemType>
vector<ItemType> LinkedBag<ItemType>::toVector() const
{
   vector<ItemType> bagContents;
   fillVector(bagContents, headPtr);
   return bagContents;
} // end toVector
```

Thus, after creating a vector, toVector fills it—by calling fillVector—with the data in the chain of linked nodes whose head pointer is headPtr. Finally, toVector returns the vector to the client.

To define fillVector, we need to think recursively. If the chain is empty—that is, if curPtr is nullptr—we have nothing to do. This is the base case. In the recursive step, we first add the data curPtr->getItem() to the vector and then recursively fill the vector with the chain that begins at curPtr->getNext(). The method then has the following definition:

```
template<class ItemType>
void fillVector(vector<ItemType>& bagContents, Node<ItemType>* curPtr) const
```