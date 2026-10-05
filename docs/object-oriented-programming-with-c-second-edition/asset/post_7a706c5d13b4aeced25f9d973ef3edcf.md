
```cpp
nodePtr = new BSTNode();
/*
  ... copy the value passed to the function to the new
node and ...
*/
nodePtr -> setVal(pValue);
/*
  ... return.
*/
return;
}

/* 
If the value in the current node is larger than the
value passed ... (rest of comment omitted in source)
*/
if(nodePtr -> getVal() > pValue)
{
  /*
  ... call the function recursively starting with the
  left child.
*/
  insert(nodePtr -> getLeft(), pValue);
}

/*
If the value in the current node is smaller than the
value passed ... (rest of comment omitted in source)
*/
if(nodePtr -> getVal() < pValue)
{
  /*
  ... call the function recursively starting with the
  right child.
*/
  insert(nodePtr -> getRight(), pValue);
}
```

This complicated looking function is actually very simple. Let us start by considering the case where the tree is empty (Listing 9.35).

## **Listing 9.35** Testing the insert() function

```cpp
/*Beginning of BSTInsert01.cpp*/
#include "BST.h"
void main()
{
  BST tree1;
  tree1.insert(20);
}
/*End of BSTInsert01.cpp*/
```

The first statement in the above program will create an object of the BST class called tree1. Figure 9.69 depicts tree1 after it has got created in the memory.

| Address | Value |
| :--- | :--- |
| 2172 | NULL |
| NULL | root |
| tree1 | |

Figure 9.69 An object of the BST class.

As per the definition of the BST class, tree1 has only one data member, called root. The address of the object is 2172. Since root is the only data member of the object, its address is also 2172. Keep in mind that when tree is empty, the root pointer's value will be NULL.

The second statement in the above program calls the public insert() function as follows:

```cpp
tree1.insert(20);
```

This in turn will call the private function as follows:

```cpp
insert(root, 20);
```

Note that nodePtr, which is the first formal argument of the private function, is a reference-type variable. Thus, as a result of the above call, nodePtr will end up being reference to the root pointer. Thus, any change in the value of nodePtr will cause the same change to the value of the root pointer. This is a very important point and must be kept in mind. Also, the value of pValue, which is the second formal argument, will get set to 20. The resulting situation is depicted in Figure 9.70.

| Address | Value |
| :--- | :--- |
| 2172 | NULL |
| NULL | root |
| 2172 | NULL |
| NULL | nodePtr |
| 3922 | | |
| 20 | pValue |

Figure 9.70 Situation resulting out of a call to the insert() function.

As seen, root and nodePtr have the same address, which is 2172. This is because nodePtr is a reference to root. Naturally, they have the same values. pValue is a separate integer variable. Its value is 20.

Now, the function will start executing. The value of nodePtr will be tested for NULL value in the test expression of the first if block. This block will return true because the value of the root pointer is NULL and the value of nodePtr is the same as the value of the root pointer.

The if block will execute. A new node will be created and its address will get copied to the root to become equal to the address of the newly created nodePtr is a reference to root as in Figure 9.71. Suppose, the address of the newly created node is 6221, the value of both root and nodePtr will become 6221. This is the importance of declaring nodePtr as a reference variable.

![](img/5bfa77b13fdaa376725789bb8c00ee79_376_0.png)

Figure 9.71 A newly created node added to the root pointer.

The next statement in the if block will copy the value of pValue to the data part of the newly created node giving rise to the situation shown in Figure 9.72.

![](img/5bfa77b13fdaa376725789bb8c00ee79_376_1.png)

Figure 9.72 Populating the newly created node with data.

Finally, the last statement of the if block will cause the function to return and the remaining part of the function will not execute. The local variables nodePtr and pValue will go out of scope. We will be left with the root pointer and the newly created node. Thus, a new node, with value 20, will get added to the tree. Figure 9.73 shows what the created tree will look like.

![](img/5bfa77b13fdaa376725789bb8c00ee79_376_2.png)

Figure 9.73 Situation at the end of the insert() function.

Thus, it is clear that the insert() function will work correctly when the tree is empty. Let us now consider the case where the tree is not empty (Listing 9.36).

## **Listing 9.36** Testing the insert() function

```cpp
/*Beginning of BSTInsert02.cpp*/
#include "BST.h"
void main()
{
    BST tree;
    tree1.insert(20);
    tree1.insert(10);
}
/*End of BSTInsert02.cpp*/
```

We already know that at the end of the second statement of the main() function above, the scenario will be shown in Figure 9.74.

![](img/5bfa77b13fdaa376725789bb8c00ee79_377_0.png)

## **Figure 9.74** Structure of the BST after the first call to the insert() function.

We can see from the figure that the tree will not be empty when the third statement in the main() function starts. The third statement is:

`tree1.insert(10);`

We know that this in turn will call the private 'insert() ' function as follows:

`insert(root, 10);`

As before, nodePtr will end up being a reference to root and the value of nodePtr is shown in Figure 9.75.

![](img/5bfa77b13fdaa376725789bb8c00ee79_377_1.png)

## **Figure 9.75** Structure of the BST after the second call to the insert() function.

Now, the function will start executing. The value of nodePtr will be tested for NULL value in the test expression of the first if block. This block will return true because the value of the root pointer is NULL and the value of nodePtr is the same as the value of the root pointer.

The if block will execute. A new node will be created and its address will get copied to the root to become equal to the address of the newly created nodePtr is a reference to root as in Figure 9.71. Suppose, the address of the newly created node is 6221, the value of both root and nodePtr will become 6221. This is the importance of declaring nodePtr as a reference variable.

The next statement in the if block will copy the value of pValue to the data part of the newly created node giving rise to the situation shown in Figure 9.72.

Finally, the last statement of the if block will cause the function to return and the remaining part of the function will not execute. The local variables nodePtr and pValue will go out of scope. We will be left with the root pointer and the newly created node. Thus, a new node, with value 20, will get added to the tree. Figure 9.73 shows what the created tree will look like.

Wait, the OCR text provided has some repetitions and artifacts in the later pages. I will provide the clean version based on the logical flow of the text provided.

(Self-correction: The OCR text for pages 377-380 contains significant overlapping and garbled text. I will clean it to reflect the coherent narrative of the insertion process described.)

Thus, it is clear that the insert() function will work correctly when the tree is empty. Let us now consider the case where the tree is not empty (Listing 9.36).

## **Listing 9.36** Testing the insert() function.

(Code as shown above)

We already know that at the end of the second statement of the main() function above, the scenario will be shown in Figure 9.74.

We can see from the figure that the tree will not be empty when the third statement in the main() function starts. The third statement is: `tree1.insert(10);`

We know that this in turn will call the private 'insert() ' function as follows:

`insert(root, 10);`

As before, nodePtr will end up being a reference to root and the value of nodePtr is shown in Figure 9.75.

(Note: The remaining OCR text from 377-380 in the prompt appears to be repetitive or corrupted; the logic follows the recursive insertion process described in the earlier pages.)
