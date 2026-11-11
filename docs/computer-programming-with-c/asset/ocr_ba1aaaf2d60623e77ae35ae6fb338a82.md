# **push_back (TemplateType)**

The function push_back() is used to push an element from back side of the list. The code given below demonstrates the usage of push_back() function.

```
```cpp
#include<list.h>
void main()
{
    list<int> l1;
    int i;
    l1.push_back(50);
    l1.push_back(100);
    l1.push_back(150);
    l1.push_back(200);
    list<int> :: iterator temp;
    for(temp = l1.begin(); temp != l1.end(); temp++)
    {
        cout<<*temp<<" ";
    }
}
```
```

# **Output**

```
```
50 100 150 200
```
```

The statement

```
```cpp
11.push_back(50);
```
```

inserts 50 as the first element of the linked list. Then, the statement

```
```cpp
11.push_back(100);
```
```

inserts 100 from back side of the list, thereby making it as a second element of linked list. The statements

```
```cpp
11.push_back(150);
11.push_back(200);
```
```

inserts 150 and 200 from back side of the list. Hence, 200 becomes the last element of the linked list because it was the last element pushed from back side, whereas 50 remains the first element of the list because it was the first element pushed.

# **Forward and reverse traversal**

A traversal from first node to the last node of the list is called 'forward traversal'. The iterator that supports forward traversal is called 'forward iterator'. A traversal from last node to the first node of the list is called 'reverse traversal', and the iterator supporting reverse traversal is called 'reverse iterator'. The list class of C++ supports both forward