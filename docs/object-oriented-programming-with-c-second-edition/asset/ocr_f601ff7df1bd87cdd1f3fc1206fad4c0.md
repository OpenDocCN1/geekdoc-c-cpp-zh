# Object-Oriented Programming with C++

Let us come back to the definition of the insert() function after understanding the calling pattern that we observe here. Please keep in mind that the functions of the BST class that carry the actual task are recursive and need the root pointer to be passed as an parameter to them. But, at the same time, we cannot expect the programs that use the BST class to pass the value of the root pointer when they call its functions (they have no way of knowing the value of the root pointer).

So, what is the way out? The problem can be solved by creating a public function that does not expect the root pointer to be passed to it, but in turn calls a private function, which does the actual work, and passes the root pointer to it. We are able to ensure that the functions that do the actual get the root pointer as a parameter, without expecting the calling program to pass it for it.

For example, if tree1 is an instance of the BST class (created in one of the user programs of the BST class) and we need to insert the value 20 into the tree, then the public insert() function will be called as follows:

```
tree1.insert(20);
```

The definition of the public insert() function is as follows:

```
/*
Function to insert a node at the correct place in the
BST.
*/
void BST::insert(int pValue)
{
/*
Call the private function to insert the node at the
correct place in the BST.
*/
insert(root, pValue);
}
```

As can be seen, the public function in turn calls the private function. It transfers the data value that passed to it to the private function. It also passes the value of the root pointer to the private function.

Let us look at the definition of the private version of this function, which does the actual work for it.

```
/*
Private function to insert the node. Will be called from
the public function.
*/
void BST::insert(BSTNode * &nodePtr, int pValue)
{
/*
Reference to a pointer is passed as one parameter.
*/
/*
If the pointer == NULL ...
*/
if(nodePtr == NULL)
{
/*
... create a node and make the pointer point at it
and ...
*/
```