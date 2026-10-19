what someone is doing with a linked list without having to figure out why one genericLink variable is used over and over again or what pointer->next->last->next is pointing at. Consider this code fragment:

```
C++ Example of Traditional Node Insertion Code
void InsertLink(
    Node *currentNode,
    Node *insertNode
) {
    // insert "insertNode" after "currentNode"
    insertNode->next = currentNode->next;
    insertNode->previous = currentNode;
    if ( currentNode->next != NULL ) {
        currentNode->next->previous = insertNode;
    }
    currentNode->next = insertNode;
}
```

This line is needlessly difficult.

This is traditional code for inserting a node in a linked list, and it’s needlessly hard to understand. Inserting a new node involves three objects: the current node, the node currently following the current node, and the node to be inserted between them. The code fragment explicitly acknowledges only two objects: insertNode and currentNode. It forces you to figure out and remember that currentNode->next is also involved. If you tried to diagram what is happening without the node originally following currentNode, you would get something like this:

![](bbox=[0.22, 0.51, 0.42, 0.54])

A better diagram would identify all three objects. It would look like this:

![](bbox=[0.22, 0.6, 0.6, 0.63])

Here’s code that explicitly references all three of the objects involved:

```
C++ Example of More Readable Node-Insertion Code
void InsertLink(
    Node *startNode,
    Node *newMiddleNode
) {
    // insert "newMiddleNode" between "startNode" and "followingNode"
    Node *followingNode = startNode->next;
    newMiddleNode->next = followingNode;
    newMiddleNode->previous = startNode;
    if ( followingNode != NULL ) {
        followingNode->previous = newMiddleNode;
    }
    startNode->next = newMiddleNode;
}
```