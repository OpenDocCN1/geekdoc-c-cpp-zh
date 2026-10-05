# Object-Oriented Programming with C++

|2172 |
| NULL | root |
| tree1 |

Figure 9.69 An object of the BST class

As per the definition of the BST class, tree1 has only one data member, called root. The address of the object is 2172. Since root is the only data member of the object, its address is also 2172. Keep in mind that when tree is empty, the root pointer's value will be NULL.
The second statement in the above program calls the public insert() function as follows:

```
tree1.insert(20);
```

This in turn will call the private function as follows:

```
insert(root, 20);
```

Note that nodePtr, which is the first formal argument of the private function, is a reference-type variable. Thus, as a result of the above call, nodePtr will end up being reference to the root pointer. Thus, any change in the value of nodePtr will cause the same change to the value of the root pointer. This is a very important point and must be kept in mind. Also, the value of pValue, which is the second formal argument, will get set to 20. The resulting situation is depicted in Figure 9.70.

|2172 |
| NULL | root |
|2172 |
| NULL | nodePtr |
|3922 |
| 20 | pValue|

Figure 9.70 Situation resulting out of a call to the insert() function

As seen, root and nodePtr have the same address, which is 2172. This is because nodePtr is a reference to root. Naturally, they have the same values. pValue is a separate integer variable. Its value is 20.
Now, the function will start executing. The value of nodePtr will be tested for NULL value in the test expression of the first if block. This block will return true because the value of the root pointer is NULL and the value of nodePtr is the same as the value of the root pointer.
The if block will execute. A new node will be created and its address will get copied to the root to become equal to the address of the newly created nodePtr is a reference to root as in Figure 9.71. Suppose, the address of the newly created node is 6221, the value of both