
```cpp
{
    move = move->next;
    steps++;
}

node* new_node = new node;       //create a new node;
new_node->data = data;

if(position == 1)       //if node is to be inserted at the first place
{
    new_node->next = start;
    start = new_node;
}
else
{
    new_node->next = move->next;
    move->next = new_node;
}
}

void main()
{
    int value, data, choice, position, total = 0;
    link_list link;
    cout << "Enter the elements of the list terminated by negative number :\n";
    cin >> value;
    do
    {
        link.create(value);
        total++; //increment with every node inserted;
        cin >> value;
    }
    while(value >= 0);
    cout << "\n\nThe list before any operation is performed (LIFO) :\n";
    link.display(0);
    cout << "\n\nTotal node := " << total;
    cout << "\n\nEnter the position where node is to be inserted :";
    cin >> position;
    if(position <= 0 || position > total + 1) //check for valid position
    {
        cout << "\nWrong position inputted\n";
        exit(1);
    }
    cout << "\n\nEnter the value of the node to be inserted :=";
    cin >> data;
    link.insert(position, data);
    cout << "\nThe list after insertion is :\n";
    link.display(1);
}
```

### 输出：

```text
Enter the elements of the list terminated by negative number :
10 20 30 40 50 60 -2

The list before any operation is performed (LIFO) :
60->50->40->30->20->10->NULL

Total node := 6

Enter the position where node is to be inserted :3

Enter the value of the node to be inserted :=90

The list after insertion is :
60->50->90->40->30->20->10->NULL
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_716_0.png)

图 15.17. 程序的输出屏幕。

## 程序：从链表中删除一个节点

```cpp
#include <iostream.h>
#include <process.h>    //for exit() function

struct node
{
    int data;              //data field
    node* next;            //pointer to the next node
};

class link_list
{
private:
    node* start;
public:
    link_list()             //constructor
    {
        start = NULL;       //initially the list has no node
    }
    void create(int i)
    {
        node* new_node = new node;       //create a new node
        new_node->data = i;
        new_node->next = start;          //make new node to point
                                         //to the first node
        start = new_node;                //make new node as the
                                         //first node in the list
    }
    void display(int);                   //function prototype
    void remove(int);                    //function prototype
};                                      //end of class

//function definition display()
void link_list::display(int delete_node)
{
    node* move = start;
    node* temp;
    while(move)
    {
        cout << move->data << "->";     //display the data
        temp = move;
        move = move->next;               //move to next node
        if(delete_node)
            delete(temp);
    }
    cout << "NULL";
}

//function definition remove()
void link_list::remove(int position)
{
    node* move = start;
    int steps = 1;
    while(steps < position - 1)
    {
        move = move->next;
        steps++;
    }
    if(position == 1)    //if the node to be deleted is at the first place
    {
        node* temp = start;
        start = start->next;
        delete(temp);
    }
    else
    {
        node* temp = move->next;
        move->next = move->next->next;
        delete(temp);
    }
}

void main()
{
    int value, data, choice, number, total = 0;
    link_list link;
    cout << "Enter the elements of the list terminated by negative number :\n";
    cin >> value;
    do
    {
        link.create(value);
        total++;  //increment with every node inserted
        cin >> value;
    }
    while(value >= 0);
    cout << "\nThe list before any operation is performed (LIFO) :\n";
    link.display(0);
    cout << "\nTotal node := " << total;
    cout << "\n\nEnter the number of the node to be deleted :=";
    cin >> number;
    if(number <= 0 || number > total) //check for valid position
    {
        cout << "\nWrong number input";
        exit(1);
    }
    total--;
    link.remove(number);
    cout << "\n\nThe list after deletion is :\n";
    link.display(1);
    cout << "\n\nTotal nodes := " << total;
}
```

### 输出：

```text
Enter the elements of the list terminated by negative number :
10 20 30 40 50 60 -70

The list before any operation is performed (LIFO) :
60->50->40->30->20->10->NULL

Total node := 6

Enter the number of the node to be deleted :=3

The list after deletion is :
60->50->30->20->10->NULL

Total nodes := 5
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_719_0.png)

## 程序：创建并遍历双向链表

```cpp
#include <iostream.h>

struct doubly
{
    int data;
    doubly* back;
    doubly* front;
};

class doubly_class
{
private:
    doubly* start;
public:
    doubly_class()
    {
        start = new doubly;
        start->front = NULL;
        start->back = NULL;
        start->data = -1;      //header node - can contain
                               //other information also
    }
    void create();          //function prototype
    void display();         //function prototype
};

//function definition create()
void doubly_class::create()
{
    int value;
    doubly* new_node = new doubly;
    new_node = start;
    cout << "Enter the data terminated by negative number :\n";
    cin >> value;
    while(value >= 0)
    {
        new_node->front = new doubly;
        new_node->front->back = new_node;
        new_node = new_node->front;
        new_node->data = value;
        new_node->front = NULL;
        cin >> value;
    }
}

//function definition display()
void doubly_class::display()
{
    cout << "\n\nTraversing in the forward direction :\n\n";
    doubly* move = start;
    do
    {
        move = move->front;
        cout << move->data << " <-> ";
    }
    while(move->front);
    cout << "NULL";
    cout << "\n\nTraversing in the back direction :\n\n";
    do
    {
        cout << move->data << " <-> ";
        move = move->back;
    }
    while(move->back);
    cout << "NULL";
}

void main()
{
    doubly_class d_list;    //creation of an object for
                            //doubly_class
    d_list.create();
    d_list.display();
}
```

### 输出：

```text
Enter the data terminated by negative number :
20 30 10 40 60 50 -90

Traversing in the forward direction :
20 <-> 30 <-> 10 <-> 40 <-> 60 <-> 50 <-> NULL

Traversing in the back direction :
50 <-> 60 <-> 40 <-> 10 <-> 30 <-> 20 <-> NULL
```

## 程序：在双向链表的第一个位置插入一个节点

```cpp
#include <iostream.h>

struct doubly
{
    int data;
    doubly* back;
    doubly* front;
};

class doubly_class
{
private:
    doubly* start;
public:
    doubly_class()
    {
        start = new doubly;
        start->front = NULL;
        start->back = NULL;
        start->data = -1;
    }
    void create();
    void insert_first(int data)
    {
        doubly* temp = new doubly;
        temp->data = data;
        temp->front = start->front;
        start->front->back = temp;
        temp->back = start;
        start->front = temp;
    }
    void display();
};

void doubly_class::create()
{
    int value;
    doubly* new_node = new doubly;
    new_node = start;
    cout << "\nEnter the data terminated by negative number :\n";
    cin >> value;
    while(value >= 0)
    {
        new_node->front = new doubly;
        new_node->front->back = new_node;
        new_node = new_node->front;
        new_node->data = value;
        new_node->front = NULL;
        cin >> value;
    }
}

void doubly_class::display()
{
    cout << "\n\nTraversing in the forward direction :\n\n";
    doubly* move = start;
    do
    {
        move = move->front;
        cout << move->data << " <->";
    }
    while(move->front);
    cout << "NULL";
    cout << "\n\nTraversing in the back direction :\n\n";
    do
    {
        cout << move->data << " <->";
        move = move->back;
    }
    while(move->back);
    cout << "NULL";
}

void main()
{
    int value;
    doubly_class list;
    list.create();
    cout << "Before any operation :";
    list.display();
    cout << "\n\nEnter the data value of the first node :";
    cin >> value;
    list.insert_first(value);
}
```
