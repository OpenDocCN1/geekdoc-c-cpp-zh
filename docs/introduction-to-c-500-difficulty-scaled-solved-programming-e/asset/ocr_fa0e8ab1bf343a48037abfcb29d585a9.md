```
{
  cout << "Min:" << p->key << '\\n';
}
find_min(p->left);
```

In binary tree, the smallest value is stored in the left node, the recursion ends. To find the largest value, just change pointer to p->right, to find the most right node. Call the function with the root pointer, to test its operation. For an alternative recursive function, try U.14.17.

# C.14.14 Write a recursive function that functions the nodes of the tree.

```
void tree_nodes(Node *p) {
  if(p == nullptr)
    return;
  cnt++;
  tree_nodes(p->left);
  tree_nodes(p->right);
}
```

Comments: For simplicity, cnt could be a global variable initialized with 0 and incremented by one time a node is visited.

C.14.15 Modify the structure that represents the node, in order to store different strings in the tree. For example:

```
struct Node {
  char *key;
  Node *left;
  Node *right;
}
```

Modify add_node() and delete_tree().

# Answer:

```
Node* add_node(Node *p, char key[]) {
  int tmp;
  if(p == nullptr) {
    p = new Node;
    p->key = new char[strlen(key) + 1];
    strcpy(p->key, key);
    p->left = p->right = nullptr;
  } else {
    tmp = strcmp(key, p->key);
    if(tmp < 0)
      p->left = add_node(p->left, key);
  }
```