# Solutions to Chapter 13 | C++

13.8 Write a method that takes a pointer to a Node structure as a parameter and returns a complete copy of the passed-in data structure. The Node structure contains two pointers to other Nodes.

# SOLUTION

The algorithm will maintain a mapping from a node address in the original structure to the corresponding node in the new structure. This mapping will allow us to discover previously copied nodes during a depth first traversal of the structure. Traversals often mark visited nodes—the mark can take many forms and not necessarily needs to be stored in the node). Thus, we have a simple recursive algorithm:

```
typedef map<Node*, Node*> NodeMap;
Node* copy_recursive(Node* cur, NodeMap& nodeMap) {
    if(cur == NULL) {
        return NULL;
    }
    NodeMap::iterator i = nodeMap.find(cur);
    if (i != nodeMap.end()) {
        return i->second;
    }
    // we've been here before, return the copy
    }
    Node* node = new Node;
    nodeMap[cur] = node; // map current node before traversing links
    node->ptr1 = copy_recursive(cur->ptr1, nodeMap);
    node->ptr2 = copy_recursive(cur->ptr2, nodeMap);
    return node;
}
Node* copy_structure(Node* root) {
    NodeMap nodeMap; // we will need an empty map
    return copy_recursive(root, nodeMap);
}
```