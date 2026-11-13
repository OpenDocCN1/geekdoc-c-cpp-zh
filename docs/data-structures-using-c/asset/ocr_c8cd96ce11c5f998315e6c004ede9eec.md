We shall now extend the abstract notation to show the external link. Figure 15.8 illustrates the list with the external link, Head.

To represent this linked list as shown in Fig. 15.8, we represent the linked list as an object of the LinkList class. The definition of the class is shown in Program Code 15.2.

```
PROGRAM CODE 15.2
class SLL // Singly linked list
{
private:
 Node *Head;
public:
 SLL(); // Constructor
 ~SLL(); // Destructor
 void Insert(int x);
 void Display();
 :
 : } More member functions here
 :
 :
};
```

The LinkList class has only one member data item, the Head pointer to the first node of the list. The Head is used to access the list. The member functions including constructor and destructor are used to process the list. Note that the Head is private and all other member functions are public. This is because particular nodes of the list are accessible to outside objects through pointers. Nodes are made inaccessible to outside objects by declaring Head private so that the information hiding principle is not really compromised. In Program Code 15.3,

+   1. array stk[] and top are private members, which are hidden and cannot be accessed by outside functions;
+   2. methods push, pop, isFull, isEmpty are public, which can be accessed by outside functions;
+   3. the two main features data abstraction and encapsulation are satisfied in this declaration.

```
PROGRAM CODE 15.3
/*Class of stack using array*/
#define size 20
class stack
{
 int stk[size];
```