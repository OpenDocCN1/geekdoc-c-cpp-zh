```
void Node::setRight(Node* r)
{
    right=r;
}
void Node::setData(int v)
{
    data=v;
}
/*---------------------------------------------*/
```

To test the Node class, we will write a driver program that calls each of the methods at least once and prints the state of the attributes after each method is called.

```
/*---------------------------------------------*/
/* Program chapter10_6                         */
/* This program tests the node class           */
/* filename: nodeTest.cpp                      */
/*---------------------------------------------*/
#include<iostream>    //Required for cout.
#include "Node.h"     //Required for Node.
using namespace std;
```

```
int main()
{
    Node n1,n3;    //Test default constructor.
    Node n2(4);    //Test parameterized constructor.
```

```
//Test accessor methods.
cout << "Value of n1 after default construction: "
     << endl << " n1.getData() << " << n1.getData() << ","
     << " n1.getRight() << endl;
cout << "Value of n2 after parameterized construction: "
     << endl << " n2.getData() << " << n2.getData() << ","
     << " n2.getRight() << endl;
```

```
//Test mutator methods.
n1.setData(13);
n1.setLeft(n2);
n1.setRight(n3);
cout << "Value of n1 after modification: " << endl
     << " n1.getData() << " << n1.getData() << ","
     << " n1.getLeft() << endl;
cout << "Value of n2 after modification: " << endl
     << " n2.getData() << " << n2.getData() << ","
     << " n2.getRight() << endl;
cout << "Value of n3 after modification: " << endl
     << " n3.getData() << " << n3.getData() << ","
     << " n3.getRight() << endl;
return 0;
}
/*---------------------------------------------*/
```