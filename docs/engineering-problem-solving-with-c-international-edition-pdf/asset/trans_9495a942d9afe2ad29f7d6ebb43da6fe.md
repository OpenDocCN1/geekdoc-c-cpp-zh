

```cpp
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

```cpp
//Accessors
template<typename T>
Node<T>* Node<T>::getLeft() const
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

```cpp
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

请注意，类实现要求每个方法都定义为方法模板。

BinaryTree 的类模板定义如下：

```cpp
/**......................................................*/
/* Binary tree declaration                             */
/* filename: binaryTreeTemplate.h                      */
```

```cpp
#include "nodeTemplate.h" //Required for node.
#include "nodeTemplate.cpp" //Required for node implementation.
#include <iostream> //Required for ostream.
using namespace std;

template<typename T>
class BinaryTree {
public:
//Default constructor.
BinaryTree();

//public, non recursive print and insert
void print(ostream& out) const;
void insert(T value);
void clear();

private:
//private recursive overloaded print and insert
void print(ostream& out, Node<T>* rt) const;
void insert(Node<T>*& rt, T value);
void clear(Node<T>* rt);

//private attribute
Node<T>* root;
};
```

```cpp
//--------------------------------------------------------------*/
// Binary tree implementation
//--------------------------------------------------------------*/
// filename: binaryTreeTemplate.cpp
*/
```

```cpp
#include "binaryTreeTemplate.h" //Required for BinaryTree.
#include <iostream> //Required for ostream.
using namespace std;

//Constructor
template<typename T>
BinaryTree<T>::BinaryTree():root(0)
{
}

//clear: Public method
template<typename T>
void BinaryTree<T>::clear()
{
if(root == NULL)
{
return;
}
else
{
```

```cpp
clear(root); //call private clear()
root = 0; //tree is empty
}
}//end clear
```

```cpp
//clear: private, recursive method
template<typename T>
void BinaryTree<T>::clear(Node<T>* theRoot)
{
if(theRoot == NULL)
return;
else
{
clear(theRoot->getLeft());
clear(theRoot->getRight());
delete theRoot;
}
}//end clear
```

```cpp
//print: Public method
template<typename T>
void BinaryTree<T>::print(ostream& os) const
{
if(root == NULL)
{
cout << "tree is empty ";
return;
}
else
print(os, root); //call private print()
}//end print
```

```cpp
//print: private, recursive method
template<typename T>
void BinaryTree<T>::print(ostream& os, Node<T>* theRoot) const
{
if(theRoot == NULL)
return;
else
{
print(os, theRoot->getLeft());
os << theRoot->getData() << ' ';
print(os, theRoot->getRight());
}
}//end print
```

```cpp
//insert: public method
template<typename T>
void BinaryTree<T>::insert(T value)
{
if(root == NULL)
```

```cpp
root = new Node<T>(value);
else
insert(root, value); //call private insert
}//end insert

//insert private method
template <typename T>
void BinaryTree<T>::insert(Node<T>* root, T val){
if(val < root->getData())
{
//Traverse the left subtree
if(root->getLeft() == NULL)
{
//insert new node here.
root->setLeft(new Node<T>(val));
}
else
{
//recursive call to traverse left subtree
insert(root->getLeft(), val);
}
}
else
{
//Traverse the right subtree
if(root->getRight() == NULL)
{
//insert new node here
root->setRight(new Node<T>(val));
}
else
{
//recursive call to traverse right subtree
insert(root->getRight(), val);
}
}
}//end insert
/*--------------------------------------------------------------*/
```

通过程序员定义的类模板进行泛型编程是 C++ 编程语言的一个强大特性，但所需语法可能有点繁琐。类模板应始终从特定类实现的工作版本开发。

![](img/f2bfa570e453b020c16e048c79a3ea0e_556_0.png)

以下程序测试我们的类模板：

```cpp
/*--------------------------------------------------------------*/
/* filename: testBTree.cpp */
/*--------------------------------------------------------------*/
#include <iostream> //Required for cout.
#include "BinaryTreeTemplate.cpp" //Required for BinaryTree.
using namespace std;
```

```cpp
int main(){
BinaryTree<int> bt; //Test default constructor
bt.insert(2); //Test insert on empty tree.
bt.insert(10); //Test insert to right subtree.
bt.insert(-2); //Test insert to left subtree.
bt.print(cout); //Test print method.
bt.clear(); // Test clear method.
bt.print(cout);
return 0;
}
```

测试程序的示例运行产生了以下输出：

```
-2 2 10
tree is empty
```

输出与特定定义的测试输出匹配。

### 修改！

- 1. 添加一个名为 printPreOrder(ostream&) 的公共方法和一个名为 printPreOrder(ostream&, Node*) 的私有递归方法，用于执行树的先序打印。递归先序算法如下：

```
preOrder traverse:
if(root == null)
return
visit node
preOrder traverse left child
preOrder traverse right child
```

对图 10.8 中的树进行先序打印将产生以下输出：14 10 8 22 19 17 27。

- 2. 添加一个名为 printPostOrder(ostream&) 的公共方法和一个名为 printPostOrder(ostream&, Node*) 的私有递归方法，用于执行树的后序打印。递归后序算法如下：

```
postOrder traverse:
if(root == null)
return
postOrder traverse left child
postOrder traverse right child
visit node
```

对图 10.8 中的树进行后序打印将产生以下输出：8 10 17 19 27 22 14。

## 10.6 继承

在本节中，我们将介绍 C++ 编程语言的特性，这些特性通过使用继承和虚方法支持多态性。多态性是为同一个名称赋予多种含义的能力。这是面向对象编程中的一个重要概念，因为它允许将多种不同类型的对象赋给单一类型的对象。因此，单一类型名称可以有多种含义。

继承提供了一种从现有类类型定义新类类型的机制。现有类型称为基类型，新类型称为派生类型。派生类型从基类型派生并继承基类型的属性。派生类型的对象与其基类型的对象兼容，因此基类型的对象可以赋予许多不同派生类型的值。

除了支持多态性，继承还通过继承类类型属性和方法来最大限度地重用代码。为了说明 C++ 中继承的实现，我们将开发一个 Rectangle 类和一个 Square 类，如图 10.9 所示。请注意，UML 使用开放箭头来指示继承。继承仅在箭头方向上建模 is-a 关系。重要的是要记住，正方形 is-a 矩形，但矩形不一定是正方形。

### Rectangle 类

矩形可以由宽度、高度和原点来描述。因此，类声明将需要三个私有属性以及支持这些属性的修改器和访问器方法。我们还包括一个 print 方法、一个将矩形移动到平面新位置的方法，以及一个确定矩形面积的方法。move 方法是一个修改器方法，因为它将修改调用对象的原点。计算矩形面积的方法不应修改调用对象的属性，因此我们在定义面积方法时将使用 const 修饰符。Rectangle 类的类声明如下：

![](img/f2bfa570e453b020c16e048c79a3ea0e_558_0.png)

图 10.9 UML 类层次结构。

