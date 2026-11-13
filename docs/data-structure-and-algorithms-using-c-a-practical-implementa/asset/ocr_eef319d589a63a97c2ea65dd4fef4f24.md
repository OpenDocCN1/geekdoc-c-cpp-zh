```
cout<<setw(5)<<node->info;
node = node->next;
}
}
```

```
void sort(struct link *node)
{
 for(New = start.next; New->next != NULL; New =
New->next)
{
 for(temp = New->next; temp != NULL; temp =
temp->next)
{
 if(New->info > temp->info)
{
 int t = New->info;
 New->info = temp->info;
 temp->info = t;
}
}
}
}
```

# OUTPUT

```
ENTER A NUMBER : 58
DO YOU WANT TO CRETATE MORE NODES : y
ENTER A NUMBER : 7
DO YOU WANT TO CRETATE MORE NODES : y
ENTER A NUMBER : 65
DO YOU WANT TO CRETATE MORE NODES : y
ENTER A NUMBER : 3
DO YOU WANT TO CRETATE MORE NODES : y
ENTER A NUMBER : 11
DO YOU WANT TO CRETATE MORE NODES : n
THE CREATED LINKED LIST IS :
58 7 65 3 11
AFTER SORT THE LINKED LIST IS :
3 7 11 58 65
Process exited after 59.188 seconds with return value 0
Press any key to continue . . .
```