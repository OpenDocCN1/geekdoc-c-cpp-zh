
Example:
```
template<typename Dtype>
void swapTwo(Dtype& a, Dtype& b)
{
    Dtype temp = a;
    a = b;
    b = temp;
}

Prototype:
template<typename Dtype>
void swapTwo(Dtype& a, Dtype& b);
```

The keyword template, followed by a parameter list enclosed within <> symbols, must precede a function template definition and a function template prototype. Within the parameter list the keyword typename precedes each identifier in the list, indicating that the identifier represents a data type. The template parameter list must include at least one parameter. If multiple parameters are used, they are separated with commas, as in:

```
template <typename T1, typename T2, typename T3>
```

The following program calls the function template minVal() four times to find the smallest value in arrays of type int, char, double, and string.

```
/*********************************************************************/
/* Program chapter10_7 */
/* This program demonstrates the use of the function */
/* template minVal. */
/*********************************************************************/
#include<iostream> //Required for cout.
#include<string> //Required for string.
using namespace std;
//Function Prototype:
template <typename Dtype>
Dtype minVal(const Dtype x[], int n);
int main()
{
//Declare objects.
const int SIZE = 10;
char cInt[SIZE] = {'h','e','l','l','o',' ','w','o','r','l','d'};
int iDat[SIZE] = {5,2,7,8,2,5,9,8,1,9};
double dDat[SIZE] = {-2.1,4.3,0.0,9.3,0.4,-4.2};
string sDat[SIZE] = {"this","short","the","list","of","strings"};
//Print smallest value in each array.
cout << "smallest value in each array."
<< endl << minVal(cInt,SIZE) << endl; // Char
cout << "smallest integer in iDat is "
<< minVal(iDat, SIZE) << endl; // int
cout << "smallest double in dDat is "
<< minVal(dDat, 6) << endl; // double
cout << "smallest string in sDat is: "
<< minVal(sDat, 6) << endl; // string

return 0;
/*--------------------------------------------------------------*/
```

The output from a sample run is given below:
smallest char in ch is: d
smallest integer in iDat is: 1
smallest double in dDat is: -4.2
smallest string in sDat is: list

The function template minVal() uses two operators, < and =, to find the smallest value in the array, x. Thus, minVal() can be called with any data type that has these operators defined. The operator, =, is, by default, defined for all types, but the same is not true for the operator <. If we tried to call minVal() with an array of type Card, for example, the result would be a long list of compiler errors because we did not overload this operator in our Card class definition.

We can add a boolean method to our Card class to overload the < operator, if we can define what it means for one card to be less than another card. When overloading the operator < for a new type, it should always hold that if c1 < c2 and c2 < c3 then c1 < c3 for all objects of the type. This is true for all relational operators.

![](img/0235a4ea835dc4575bd036e024a533b3_622_0.png)

## Practice 10.4

Questions 1-4 refer to the functions defined in Section 7.1.

- 1. Write a function template for the function:

```
double mean(const double x[], int n);
```

Test your template with at least 2 data types.

- 2. Write a function template for the function:

```
double median(const double x[], int n);
```

Test your template with at least 2 data types.

- 3. Write a function template for the function:

```
double variance(const double x[], int n);
```

Test your template with at least 2 data types.

## Practice 10.4 continued

4. Write a function template for the function:

```
double std_dev(const double x[], int n);
```

Test your template with at least 2 data types.

## Class Templates

In Section 10.5, we developed a working version of a BinaryTree class. We will use this class to develop a class template to represent a generic binary tree, and test it against the working version.

The declaration of a class template must begin with an expression of the form:

```
template < typename identifier >
```

as illustrated in the following declaration of a class template to represent a node on a binary tree:

```
/**
 * class declaration for Node template:
 * filename nodeTemplate.h
 */

#ifndef TNODE_H
#define TNODE_H

template<typename T>
class Node
{
    //Private attributes
    private:
        T data;
        Node *left;
        Node *right;

    //Public interface.
    public:
        Node(); //Default constructor
        Node(T); //Parameterized constructor

        //Accessors
        Node* getLeft() const;
        Node* getRight() const;
        T getData() const;

        //Mutators
        void setLeft(Node*);
        void setRight(Node*);
        void setData(T v);
};
#endif
/***********************************************************************/
```

Notice that the identifier T replaces int in the class template declaration. The implementation of this class template follows.

```
/***********************************************************************/
/* Class implementation for Node template */
/* filename: nodeTemplate.cpp */
/*
#include "nodeTemplate.h" //Required for Node.
using namespace std;

//Constructors.
template<typename T>
Node<T>::Node() : data(0), left(nullptr), right(nullptr)
{
}
template<typename T>
Node<T>::Node(T v):data(v), left(nullptr), right(nullptr)
}

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
}

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
/******************************************************************/
```

Notice that the class implementation requires that each method be defined as a method template.

The class template definition for BinaryTree follows:

```
/******************************************************************/
/* Binary tree declaration
/* filename: binaryTreeTemplate.h
/*
/******************************************************************/

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
}
/*------------------------------------------------------------*
 *                        *
 *  Binary tree implementation                            *
 *  Filename: binaryTreeTemplate.cpp                        *
 *                        *
 *------------------------------------------------------------*/
#include "binaryTreeTemplate.h" //Required for BinaryTree.
#include <iostream>    //Required for ostream.
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
    if(root == nullptr)
    {
        return;
    }
    else
    {
        clear(root);    //call private clear()
        root = nullptr;    //tree is empty
    } //end clear
}

//clear: private, recursive method
template<typename T>
void BinaryTree<T>::clear(Node<T>* theRoot)
{
    if(theRoot == nullptr)
        return;
    else
    {
        clear(theRoot->getLeft());
        clear(theRoot->getRight());
        delete theRoot;
    } //end clear
}

//print: Public method
template<typename T>
void BinaryTree<T>::print(ostream& os) const
{
