according to its normal definition. For instance, ‘+’ operator is defined to sum two integer number. However, it can also be used to concatenate the two strings or to join the two link list. Similarly, ++ operator can be used to move to the next node of the link list. Operator ‘=’ can also be used to compare the number of nodes in two link list. It returns whether compared link list are equal in length or not.

We can use the ‘+’ operator to join two link list. In our case, we would like to write the statement, List3=list1+list2, this should result in list3 that should consist of both list1 and list2. To accomplish the above objective, the code is written below:

```
list operator +(list l2)
{
while(first->next!=NULL)        // Move to the last node of the list1
first=first->next;
first->next=l2.first;  // connect the last node to the first node
of list l2
return *this;     // return the first list
}
```

To achieve the above task, first we need to create the list l1 and the list l2. Afterwards, we can call them using the + overloaded operator. Code for the main function is described below:

```
int main()
{
list l1, l2, l3;
l1.create_beg(10);
l1.create_beg(20);
l2.create_beg(6);
l2.create_beg(33);
l3=l1+l2;
```

Using the same method, other operators like ==, < , > etc can be used. Readers are advised to write the program of operator overloading for the aforementioned operator.

# 3.9 SELF-ORGANIZING LIST

Link list is the linear data structure,as a reslt, whenever user needs to carry out any operation, he has to start from the first node and traverse the subsequent node one after another node till target node is not reached or list is exhausted. Therefore, efficiency of a list is dependent on the size of a list. If the list is large in that case, efficiency of the link list drops. To overcome this limitation, a new version of link list known as self-organizing list is devised. Self-organizing list is capable of reorganizing the node based on its usage criterian. Consequently, it yields better performance relative to the normal link list.