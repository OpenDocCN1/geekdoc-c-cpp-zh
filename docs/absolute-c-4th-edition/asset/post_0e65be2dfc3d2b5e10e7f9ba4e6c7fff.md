
## Display 17.25 Implementation File for a Tree Template Class (part 2 of 2)

```
44        inorderShow(subTreeRoot->rightLink);
45    }
46 }

47    template<class T> //uses iostream:
48    void SearchTree<T>::inorderShow( ) const
49    {
50        inorderShow(root);
51    }

52    template<class T>
53    void SearchTree<T>::deleteSubtree(TreeNode<T>*& subTreeRoot)
54    {
55        if (subTreeRoot != NULL)
56        {
57            deleteSubtree(subTreeRoot->leftLink);
58
59            deleteSubtree(subTreeRoot->rightLink);
60
61            //subTreeRoot now points to a one node tree.
62            delete subTreeRoot;
63            subTreeRoot = NULL;
64        }
65    }

64    template<class T>
65    SearchTree<T>::~SearchTree( )
66    {
67        deleteSubtree(root);
68    }
69 }//TreeSavitch
```

Uses postorder traversal of the tree.

## Self-Test Exercises

20. Define the following member functions, which could be added to the class SearchTree in Display 17.24. These functions display the data encountered in a preorder and postorder traversal of the tree, respectively. Define a private helping function for each function, as we did for SearchTree<T>::inorderShow.

void SearchTree<T>::preorderShow( ) const
void SearchTree<T>::postorderShow( ) const

## Display 17.26 Demonstration Program for the Tree Template Class

```
//Demonstration program for the Tree template class.
#include <iostream>
#include "tree.h"
#include "tree.cpp"
using std::cout;
using std::cin;
using std::endl;
using TreeSavitch::SearchTree;

int main()
{
    SearchTree<int> t;

    cout << "Enter a list of nonnegative integers.\n"
         << "Place a negative integer at the end.\n";
    int next;
    cin >> next;
    while (next >= 0)
    {
        t.insert(next);
        cin >> next;
    }

    cout << "In sorted order: \n";
    t.inorderShow();
    cout << endl;

    return 0;
}
```

### SAMPLE DIALOGUE

Enter a list of nonnegative integers.
Place a negative integer at the end.
40 30 20 10 11 22 33 44 -1
In sorted order:
10 11 20 22 30 33 40 44

## Chapter Summary

+   - A node is a struct or class object that has one or more member variables that are pointer variables. These nodes can be connected by their member pointer variables to produce data structures that can grow and shrink in size while your program is running.
+   - A linked list is a list of nodes in which each node contains a pointer to the next node in the list.
+   - The end of a linked list (or other linked data structure) is indicated by setting the pointer member variable equal to NULL.
+   - A stack is a first-in/last-out data structure. A queue is a first-in/first-out data structure. Both can be implemented using a linked list.
+   - An iterator is a construct (typically an object of some iterator class) that allows you to cycle through data items stored in a data structure.
+   - A tree is a data structure whose nodes have two (or more) member variables for pointers to other nodes. If a tree satisfies the Binary Search Tree Storage Rule, then a function can be designed to rapidly find data in the tree.

## ANSWERS TO SELF-TEST EXERCISES

1. Sally
Sally
18
18

Note that (*head).name and head->name mean the same thing. Similarly, (*head).number and head->number mean the same thing.

2. The best answer is

```
head->next = NULL;
```

However, the following is also correct:

```
(*head).next = NULL;
```

3. head->item = "Wilbur's brother Orville";

```
4. class NodeType
{
public:
NodeType() {}
NodeType(char theData, NodeType* theLink)
: data(theData), link(theLink){}
NodeType* getLink() const { return link; }
char getData() const { return data; }
void setData(char theData) { data = theData; }
```

```
void setLink(NodeType* pointer) { link = pointer; }
private:
    char data;
    NodeType *link;
};

typedef NodeType* PointerType;
```

+   5. The value NULL is used to indicate an empty list.

+   6. p1 == p1->next;

+   7. Pointer discard;
+      discard = p2->next; // discard points to the node to be deleted.
+      p2->next = discard->next;
+   
+      This is sufficient to delete the node from the linked list. However, if you are not using this node for something else, you should destroy the node with a call to delete as follows:
+   
+      delete discard;

+   8. p1 = p1->getLink( );

+   9. Pointer discard;
+      discard = p2->getLink( ); // points to node to be deleted.
+      p2->setLink(discard->getLink( ));
+   
+      This is sufficient to delete the node from the linked list. However, if you are not using this node for something else, you should destroy the node with a call to delete as follows:
+   
+      delete discard;

+   10. a. Inserting a new item at a known location into a large linked list is more efficient than inserting into a large array. If you are inserting into a list, you have about five operations, most of which are pointer assignments, regardless of the list size. If you insert into an array, on the average you have to move about half the array entries to insert a data item.
+   
+       For small lists, the answer is c, about the same.

+   11. Note that this function is essentially the same as headInsert in Display 17.11.

```
template<class T>
void Stack<T>::push(T stackFrame)
{
    top = new Node<T>(stackFrame, top);
}
```

+   12. //Uses cstddef:
+       template<class T>
+       Stack<T>::Stack(const Stack<T>& aStack)
+       {
+           if (aStack.isEmpty( ))

```
top = NULL;
else
{
    Node<Ts> *temp = aStack.top;//temp moves
    //through the nodes from top to bottom of aStack.
    Node<Ts> *end;//Points to end of the new stack.

    end = new Node<T>(temp->getData(), NULL);
    top = end;
    //First node created and filled with data.
    //New nodes are now added AFTER this first node.

    temp = temp->getLink();//move temp to second node
    //or NULL if there is no second node.
    while (temp != NULL)
    {
        end->setLink(
            new Node<T>(temp->getData(), NULL));
        temp = temp->getLink();
        end = end->getLink();
    }
    //end->link == NULL;
}

13. template<class Ts>
Stack<T>& Stack<T>::operator =(const Stack<T>& rightSide)
{
    if (top == rightSide.top) //if two stacks are the same
        return *this;
    else //send left side back to freestore
    {
        T next;
        while (! isEmpty())
            next = pop();//remove calls delete.
    }

    if (rightSide.isEmpty())
    {
        top = NULL;
        return *this;
    }
    else
    {
        Node<Ts> *temp = rightSide.top;//temp moves through
        //the nodes from front top to bottom of rightSide.
        Node<Ts> *end;//Points to end of the left-side stack.
        end = new Node<T>(temp->getData(), NULL);
```

```
top = end;;
//First node created and filled with data.
//New nodes are now added AFTER this first node.

temp = temp->getLink();//Move temp to second node
//or set to NULL if there is no second node.

while (temp != NULL)
{
    end->setLink(
        new Node<T>(temp->getData(), NULL));
    temp = temp->getLink();
    end = end->getLink();
}
//end->link == NULL;

    return *this;
}
```

14. The following should be placed in the namespace QueueSavitch:

```
//Uses cstddef:
template<class T>
Queue<T>::Queue() : front(NULL), back(NULL)
{
    //Intentionally empty.
}

//Uses cstddef:
template<class T>
bool Queue<T>::isEmpty() const
{
    return (back == NULL);//front == NULL would also work
}
```

15. The following should be placed in the namespace QueueSavitch:

```
//Uses cstddef:
template<class T>
void Queue<T>::add(T item)
{
    if (isEmpty())
        front = back = new Node<T>(item, NULL);//Sets both
        //front and back to point to the only node
    else
    {
        back->setLink(new Node<T>(item, NULL));
        back = back->getLink();
```

```
//Uses cstdlib and iostream:
template<class T>
T Queue<T>::remove()
{
    if (isEmpty())
    {
        cout << "Error: Removing an item from an empty queue.\n";
        exit(1);
    }

    T result = front->getData();

    Node<T> *discard;
    discard = front;
    front = front->getLink();
    if (front == NULL) //if you removed the last node
        back = NULL;

    delete discard;

    return result;
}
```

16. The following should be placed in the namespace QueueSavitch:

```
template<class T>
Queue<T>::Queue()
{
    T next;
    while (! isEmpty())
        next = remove();//remove calls delete.
}
```

17. The following should be placed in the namespace QueueSavitch:

```
//Uses cstddef:
template<class T>
Queue<T>::Queue(const Queue<T>& aQueue)
{
    if (aQueue.isEmpty())
        front = back = NULL;
    else
    {
        Node<T> *temp = aQueue.front;//temp moves
        //through the nodes from front to back of aQueue.
        back = new Node<T>(temp->getData(), NULL);
```
