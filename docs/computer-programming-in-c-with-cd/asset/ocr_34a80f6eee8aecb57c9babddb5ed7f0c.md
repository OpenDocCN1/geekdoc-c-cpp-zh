```
```cpp
while ( toupper (Choice! = 'N'));
Back->link=NULL;

delete (Ptr);
}

void List ::SortList() // Bubble sort
{
node * P=Head;

while (P!=NULL)
{
node * Ptr=Head;

while (Ptr!=NULL)
{
if(Ptr->data >Ptr->link->data)
{
int Temp= Ptr->data;
Ptr->data =Ptr->link->data;
Ptr->link->data=Temp;
}

Ptr=Ptr->link;
}

P=P->link;
}
}// end of sort

void List :: Insert (int Data)
{
node * Ptr=Head;
node * Back=NULL;
node * P= new node;
P->data=Data;

while ((Ptr!=NULL) &&( Data > Ptr->data))
{
Back=Ptr;
Ptr=Ptr->link;
```
```