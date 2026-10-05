```
*/
insert(nodePtr -> getLeft(), pValue);
}
```

> /*
If the value in the current node is smaller than the
value passed
*/
if(nodePtr -> getVal() < pValue)


```
{
call the function recursively starting with the
right child.
*/
insert(nodePtr -> getRight(), pValue);
}
```

> /*
Private function to do pre-order traversal. Will be
called from the public function.
*/

```
void BST::preorder(BSTNode * nodePtr)
{
As long as the passed pointer is not NULL ...
*/
if(nodePtr != NULL)
{
*/
dis the value of the current node first ...
*/
cout << nodePtr -> getVal() << endl;
*/
... 
then call the function recursively for the left
child ...
*/
preorder(nodePtr -> getLeft());
*/
... 
then call the function recursively for the
right child.
*/
preorder(nodePtr -> getRight());
}

```

> /*
Private function to do in-order traversal. Will be called
from the public function.
*/

```
void BST::inorder(BSTNode * nodePtr)
{
*/
As long as the passed pointer is not NULL ...
*/
if(nodePtr != NULL)
{
*/
... call the function recursively for the left child
first...

```