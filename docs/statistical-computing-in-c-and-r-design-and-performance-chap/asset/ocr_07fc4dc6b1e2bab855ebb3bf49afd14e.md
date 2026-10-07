# ADT ORDERED SET

371

Listing 9.6 tree.h

```
class Tree{
    Node* Root;
    int Size;

public:
    Tree() : Root(0), Size(0){
    const Node* insert(const pair<int, int&>& pairObj);
    const Node* lookUp(const int& key) const;
    const Node* getMin() const;
    const Node* getMax() const;
    int getSize() const{return Size};
};
```

The class members are an integer Size that will contain the number of nodes in the tree and a pointer to a Node object Root will be the first node to be inserted in the tree. The class constructor is of the default variant and initializes the class members to 0 (Size) and the null pointer for (Root).

The methods for the Tree class include functions to locate the nodes in the tree with the largest(max) and smallest(getMin) keys. The tree is built using a method insert that takes a pair object as argument while a tree entry with a specific key value is located with the lookUp method. All of these methods return a pointer to a const Node that points to the memory location where the operation was performed or the requested key was.

To find largest or smallest key values in a Tree, one traverses the far right or left-hand branch of the tree in Algorithm 9.16. The next listing containing the code that implements these two procedures.

```
const Node* Tree::getMin() const {
Node* temp = Root;
if(temp != 0){
    while(temp->Left != 0)
        temp = temp->Left;
    }
    return temp;
}
const Node* Tree::getMax() const {
Node* temp = Root;
if(temp != 0){
    while(temp->Right != 0)
        temp = temp->Right;
    }
    return temp;
}
```

The insert and look-up methods below both move down the tree by descending from the root comparing keys to determine whether a left or right child could be the next step in the descent. The difference is in what is accomplished once the sought-after location has found.