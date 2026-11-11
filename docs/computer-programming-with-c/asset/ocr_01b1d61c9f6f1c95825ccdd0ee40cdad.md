# # pop_front() and pop_back() methods

The function `pop_front()` deletes the front element of the linked list and the function `pop_back()` deletes the back element of the linked list. Following program demonstrates the usage of `pop_front()` and `pop_back()` functions:

```
```cpp
#include<list.h>
#include<iostream.h>
   void main()
   {
       list<int> l1;
       int i;
   l1.push_back(50);
   l1.push_back(100);
   l1.push_back(150);
   l1.push_back(200);
   cout<<"Front element is "<<l1.front()<<endl;
   cout<<"Back element is "<<l1.back()<<endl;
   //deletion
   l1.pop_back();
   cout<<"1 element poped from back"<<endl;
   cout<<"Front element is "<<l1.front()<<endl;
   cout<<"Back element is "<<l1.back()<<endl;
   l1.pop_front();
   cout<<"1 element poped from front"<<endl;
   cout<<"Front element is "<<l1.front()<<endl;
   cout<<"Back element is "<<l1.back()<<endl;
   cout<<"Full List"<<endl;
       list<int> :: iterator temp;
       for(temp = l1.begin();temp != l1.end(); temp++)
       {
           cout<<*temp<<" ";
       }
   }
```
```

# **Output**

```
```text
Front element is 50
Back element is 200
1 element poped from back
Front element is 50
Back element is 150
1 element poped from front
Front element is 100
Back element is 150
Full List
100 150
```
```