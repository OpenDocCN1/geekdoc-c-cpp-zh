```
```cpp
flushall();
getch();
}
```
```

Q49: Write a program to input in information data in a doubly linked list. Then using the concept of classes and objects, write functions to create, sort, display, insert an element, delete an element, push an element and pop an element into and from the array.

Ans:

```
```cpp
#include<iostream.h>
#include<iomanip.h>
#include<conio.h>
#include<ctype.h>
class dnode //Declaring a class to function as a node of name dnode
{
    public: //All declarations below this are public
        dnode *ulink; /*Each node will have two links, one pointing to the upper
        node and one pointing to the lower node*/
        dnode *llink;
        int data; //Each node will have a data field to store the data
};

class dlist //Declaring a class of name dlist of type doubly linked lists
{
    clrscr();
    dnode *head1,*head2; /*Each doubly linked list will have two heads one
    pointing to the start of the list and another pointing to the end of the
    list.*/
    int n;
    public: //All declarations below this are public
            dlist();
            void create();
            void display();
            void sort();
            void insert();
            void mdelete();
            void pop();
            void push();
};

dlist::dlist()
{
    n=0;
```
```