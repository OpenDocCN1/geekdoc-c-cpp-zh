The following figures show the procedure step by step:
Step 1. Initializing pointer **cur** points to the first node of the list, while the pointer **prev** has a value of null. See the following figure.

![](bbox=[0.071, 0.188, 0.473, 0.3])

Step 2. Traversing the entire list until the pointer **cur** points to the node that contains the value of **x**, and **prev** points to the previous node. See the following figure.

![](bbox=[0.073, 0.411, 0.486, 0.486])

Step 3. Link the node pointed by pointer **prev** to the node after the **cur**’s node. See the following figure.

![](bbox=[0.073, 0.553, 0.486, 0.629])

Step 4. Remove the node pointed by **cur**. See the following figure.

![](bbox=[0.073, 0.704, 0.486, 0.776])

# *Procedure delete inside*

{ Procedure to delete the node that contains value x in the linked list. Assume the linked list is not empty.}
procedure DeleteInside (x: datatype; prev: pointer);
var cur: pointer;

```
head: pointer;
begin
  cur := head; {initialize the pointers prev and cur.}
  prev := null;
  {traverse the entire list until the pointer cur points to the node that contains value of x}
  while (cur^.info != x) do
  begin
    prev := cur;
    cur := cur^.link;
  end; {end of while}
  prev^.link := cur^.link; {linked the node pointed by prev to the node after cur’s node}
  cur := null {dispose the node pointed by cur}
end;
```

# *Implementation in C language*

Implementation of the above procedure in C language is as follows:

```
struct node
{
  int info;
  struct node * next;
}*start=NULL;
void deletepos()
{
  struct node * curr,*temp;
  int pos,i;
  if(start==NULL)
  {
    printf("\n list is empty");
    getch();
    exit(1);
  }
  printf("\n enter the position");
  scanf("%d",&pos);
  temp=start;
  for(i=0;i<pos;i++)
  {
    curr=temp;
    temp=temp->next;
    if (temp==NULL)
    {
      printf("\n wrong position");
    }
  }
  curr->next=temp->next;
  printf("\n the deleted item is %d", temp-
```