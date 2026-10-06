# 9.2 Linear Collection — 377

Then get another number from the keyboard, delete all nodes containing the number and output the data in the linked list, lastly clearing the linked list before exiting.

```
//9_7.cpp
#include <iostream>
#include "9_6.h"
#include "9_6.cpp"
namespace std;

int main()
{
    LinkedList<int> Link;
    int i, key, item;
    //Input 10 integers and insert them to the head of list one by one
    for(i=0;i<10;i++)
    {
        cin>>item;
        Link.Insert(item);
    }
    //Output the linked list
    cout << "List: ";
    Link.Reset();
    //Output the data of every node, until the end of the linked list
    while(!Link.EndOfList())
    {
        cout <<Link.Data() << " ";
        Link.Next();//Let currPtr pointed to the next node
    }
    //Input the number to delete
    cout << "Please input the number to delete: ";
    cin >> key;

    //Find and delete the node
    Link.Reset();
    while (!Link.EndOfList())
    {
        if(Link.Data() == key)
            Link.DeleteAt();
        Link.Next();
    }
}
```