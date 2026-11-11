
```cpp
static int posx=40,posy=8,x=40,y=8;

class node
{
public:
node *leftchild;
int data;
node *rightchild;
node()
{
leftchild= NULL;
rightchild=NULL;
data=0;
}
};

class btree:public node
{
int depth;

char choice;
int leaf;

public:

node *root;
btree()
{
root= NULL;
leaf=0;
depth=0;
}

void insert(node ** ,int);
void insertnode(node ** ,int);
void inorder(node *);
void preorder(node *);
void postorder(node *);
void delnode(node **,int);
int leaves(node *);
int depths(node *);

};

void btree::insert(node **sr,int num)
{
        if(*sr == NULL)
        {
                *sr=new node;
                (*sr)->leftchild=NULL;
                (*sr)->data=num;
                (*sr)->rightchild=NULL;
        }
        else
        {
                if (num<(*sr)->data)
                        insert(&((*sr)->leftchild),num);
                else
                        insert(&((*sr)->rightchild),num);
        }
}

void btree::insertnode(node **sr,int num)
{
        if(*sr == NULL)
        {
                *sr=new node;
                (*sr)->leftchild=NULL;
                (*sr)->data=num;
                (*sr)->rightchild=NULL;
        }
        else
        {
                if (num<(*sr)->data)
                        insertnode(&((*sr)->leftchild),num);
                else
                        insertnode(&((*sr)->rightchild),num);
        }
}

void btree::inorder(node *sr)
{
        if (sr!= NULL)
        {
                inorder(sr->leftchild);
                cout<<"\n\t"<<sr->data;
                inorder(sr->rightchild);
        }
}

void btree::preorder( node *sr)
{
if (sr!= NULL)
{
if(sr->leftchild==NULL && sr->rightchild==NULL)
leaf++;
cout<<endl<<"\t"<<sr->data;
preorder(sr->leftchild);
preorder(sr->rightchild);
}
}

int btree::depths( node *sr)
{
if (sr!= NULL)
{
depth++;
depths(sr->leftchild);
depths(sr->rightchild);
}
return(depth);
}

void btree::postorder( node *sr)
{
if (sr!= NULL)
{
postorder(sr->leftchild);
postorder(sr->rightchild);
cout<<"\n\t"<<sr->data;
}
}

int btree::leaves( node *sr)
{
if (sr!= NULL)
{
if(sr->leftchild==NULL && sr->rightchild==NULL)
leaf++;
leaves(sr->leftchild);
leaves(sr->rightchild);
}
return(leaf);
}

void btree::delnode(node **sr,int num)
{
int found=0;
*sr=root;
node *ptr,*parent,*succ;

if(*sr==NULL)
{
        gotoxy(25,12);
        cout<<"Tree is Empty";
        return;
}

parent = ptr = NULL;
struct node *q;
q= *sr;
ptr = NULL;
parent=q;
while(q!=NULL)
{
        if(q->data==num)
        {
                found=1;
                ptr=q;
                break;
        }
        else
        {
                if(q->data>num)
                {
                        parent=q;
                        q=q->leftchild;
                }
                else
                {
                        parent=q;
                        q= q->rightchild;
                }
        }
}

if(!found)
{
    gotoxy(25,12);
    cout<<"Number is not in the tree";
    return;
}

if(ptr->leftchild==NULL && ptr->rightchild==NULL)
{
    if(parent->rightchild==ptr)
        parent->rightchild=NULL;
    else
        parent->leftchild=NULL;

    free(ptr);
}
else
if(ptr->leftchild==NULL && ptr->rightchild!=NULL)
{
    if(parent->leftchild==ptr)
        parent->leftchild=ptr->rightchild;
    else
        parent->rightchild=ptr->rightchild;

    free(ptr);
}
else
if(ptr->leftchild!=NULL && ptr->rightchild==NULL)
{
    if(parent->leftchild==ptr)
        parent->leftchild=ptr->leftchild;
    else
        parent->rightchild=ptr->leftchild;

    free(ptr);
}
else
if(ptr->leftchild!=NULL && ptr->rightchild!=NULL)
{
    parent= ptr;
    succ= ptr->rightchild;
    if(succ->leftchild==NULL && succ->rightchild!=NULL)
    {
        ptr->data=succ->data;
        ptr->rightchild=succ->rightchild;
        succ->rightchild=NULL;
        free(succ);
    }
    else
        if(succ->leftchild==NULL && succ->rightchild==NULL)
        {
            ptr->data=succ->data;
            ptr->rightchild=NULL;
            free(succ);
        }
        else
        {
            while(succ->leftchild!=NULL)
            {
                parent=succ;
                succ = succ->leftchild;
            }
            ptr->data= succ->data;
            parent->leftchild=NULL;
            free(succ);
        }
}
}

void main()
{
clrscr();
int gd = DETECT,gm;
initgraph(&gd,&gm,"");
setbkcolor(BLUE);
setcolor(RED);
cleardevice();
int choice=0;
btree a;
cout << endl;
while(choice !=8)
{
    cleardevice();
    rectangle(20,20,620,450);
    gotoxy(35,10);
    cout<<"BINARY TREE";
    gotoxy(20,11);
    cout << "1. Create Binary Tree" << endl;
    gotoxy(20,12);
    cout << "2. Insert a new node in binary tree"<< endl;
    gotoxy(20,13);
    cout << "3. Delete a node from binary tree" << endl;
    gotoxy(20,14);
    cout << "4. Display binary tree in preorder traversal" << endl;
    gotoxy(20,15);
    cout << "5. Display binary tree in inorder traversal" << endl;
    gotoxy(20,16);
    cout << "6. Display binary tree in postorder traversal" << endl;
    gotoxy(20,17);
    cout<<"7. Number of Leaves in Tree "<<endl;
    gotoxy(20,18);
    cout << "8. QUIT" << endl;
    setcolor(WHITE);
    outtextxy(150,440,"Arvind Amit Ajay Shyam JaiPrakash");
    setcolor(RED);
    gotoxy(25,22);
    cout << "Enter your option : ";
    cin >> choice ;

    switch(choice)
    {
        case 1:
            while(1)
            {
                cleardevice();
                rectangle(20,20,620,450);
                gotoxy(30,10);
                cout<<"Insert data : ";
                int data;
                cin>>data;
                if(data<0)
                {
                    gotoxy(30,12);
                    cout<<"Enter only positive numbers  ";
                    getch();
                    continue;
                }
                a.insertnode(&a.root,data);
                cout<<"                Do u wish to continue Y/N"<<endl;
                char ch=getch();
                if(ch=='n'||ch=='N')
                    break;
            }
            break;

        case 2:
            cleardevice();
            rectangle(20,20,620,450);
            gotoxy(30,10);
            cout<<"Enter the Number:  ";
            int data;
            cin>>data;
            if(data<0)
            {
                gotoxy(30,12);
                cout<<"Enter only positive numbers  ";
                getch();
                continue;
            }

            a.insert(&a.root,data);
            gotoxy(25,22);
            cout<<"press any key to continue";

            break;

        case 3:
            cleardevice();
            rectangle(20,20,620,450);
            gotoxy(25,10);
            cout<<"Enter the number to be Deleted  ";
            cin>>data;
            a.delnode(&a.root,data);
            gotoxy(25,22);
            cout<<"press any key to continue";
            int nim;
            nim = a.leaves(a.root);
            gotoxy(12,10);
            cout<<"Number of leaves are "<<nim;
            int nodes;
            nodes=a.depths(a.root);
            gotoxy(12,12);
            cout<<"Number of Nodes in Tree is "<<nodes;
            gotoxy(12,22);
            cout<<"press any key to continue";
            rectangle(20,20,620,450);
            getch();
            break;

        case 8:
            exit(1);
            break;
        default:
            cout << "Invalid Choice !! Enter Again !!";
    }
}
getch();
}
```

## D

- Data Abstraction, 3, 76, 79
- Data Access Methods, 317, 339
- data members, 254, 259, 303, 318, 320, 323, 324, 327, 328, 329, 333, 334, 335, 339, 340, 345, 348, 350, 355, 359, 368, 370, 374, 385, 391, 394, 396, 403, 437, 438, 440, 443, 468, 567
- Data types, 6, 12, 19, 20, 35, 77, 80, 81
- debugging, 11
- Declaring pointers, 212
- Declaring Pointers, 213
- decrement operators, 243, 245, 246, 247
- default argument, 170, 171, 199, 203, 347, 350, 351, 352
- Default constructor, 347, 348, 349, 350, 352, 361, 362, 363, 364
- define, 7, 8, 28, 37, 38, 39, 40, 42, 76, 78, 82, 88, 101, 106, 143, 162, 164, 183, 184, 199, 203, 253, 256, 281, 284, 292, 294, 296, 297, 300, 303, 304, 305, 306, 320, 321, 323, 324, 325, 329, 331, 338, 340, 343, 350, 369, 370, 377, 390, 396, 441, 461, 498, 527, 555, 567
- delete keyword, 218, 245
- delete operator, 65, 66, 212, 218, 219, 225, 241, 245, 246, 326, 327, 347, 363, 364, 403, 440, 441, 532, 534, 535
- Dereferencing operators, 61
- Derivations, 455, 457, 461
- Derived class constructors, 524, 569
- Derived class destructor, 473, 474, 475, 476, 477, 478, 479, 480, 561, 569
- Derived Classes, 455, 456, 461, 468, 474, 540, 546
- Derived Data Types, 35
- Destructors, 317, 344, 346, 361, 362, 363, 438, 440, 455, 468, 560
- do keyword, 116, 117
- dot (.) notation, 28
- double, 12, 15, 20, 24, 30, 31, 33, 36, 37, 39, 55, 62, 63, 65, 66, 67, 72, 85, 88, 91, 98, 99, 106, 140, 168, 184, 200, 215, 218, 219, 222, 233, 246, 254, 271, 280, 293, 295, 298, 312, 313, 314, 352, 353, 354, 403, 444, 445, 550, 556, 572, 574, 575
- do-while loop, 89, 112, 116, 117, 134
- Dynamic Binding, 322, 455, 542, 554
- Dynamic constructor, 347
- Dynamic or late binding, 543
- dynamic polymorphism, 322, 542, 543, 554, 568

## E

- Encapsulation, 3, 76, 79, 318, 320, 439, 441, 442, 566
- endl manipulator, 9, 74, 75, 96, 97, 134
- Enumeration, 26, 32, 77, 78, 82
- Error, 6, 476, 559, 560
- executable file, 6, 10, 11, 79, 80
- Exploring Other Pointer Types, 212
- Exponent, 16
- Exponential Floating Point Constants, 15
- expression, 41, 52, 54, 55, 67, 70, 102, 103, 104, 107, 108, 109, 110, 112, 113, 116, 118, 132, 134, 166, 214, 215, 410, 415, 555, 558
- extern keyword, 196, 197, 205
- External Storage Class, 196

## F

- Features of OOP, 3
- Floating Point Constants, 15, 81
- Floating Point Types, 24
- flow control, 89
- for loop, 89, 112, 119, 123, 126, 129, 134, 150, 151, 177, 181, 221, 226, 232, 540
- formal argument, 166, 203, 265
- Forms of Inheritance, 455, 485
- Fractional Floating Point Constants, 15
- Friend Classes, 317, 388, 392
- Friend Functions, 317, 388, 408, 432
- friend keyword, 388, 390
- Function Arguments, 211, 230
- function definition, 164, 166, 170, 171, 173, 183, 184, 204, 369, 372, 376, 444, 543, 544, 554, 566, 568
- Function Overloading, 322, 399, 437
