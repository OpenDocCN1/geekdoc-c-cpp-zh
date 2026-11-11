```
->info);
free(temp);
}
```

![](bbox=[0.512, 0.095, 0.932, 0.183])

# 3. Search

As long as the linked list is not empty, we can search the list for the node containing particular value e. To accomplish this operation, we need two pointers, prev and cur. After completing the searching, the pointer cur will point to the node containing the value e, and prev will hold the previous node of cur’. The following figures show the procedure step by step.

Step 1. Initializing pointer cur points to the first node of the list, while the pointer prev has a value of null. See the following figure.

![](bbox=[0.065, 0.399, 0.448, 0.427])

Step 2. Set prev point to the node pointed by cur. See the following figure.

![](bbox=[0.065, 0.522, 0.482, 0.574])

Step 3. Set cur point to the node after prev’. See the following figure.

![](bbox=[0.065, 0.677, 0.482, 0.731])

Step 4. Repeat step 2, step 3, until cur is pointing to the node that contains value. See the following figures.

![](bbox=[0.065, 0.835, 0.482, 0.891])

# Procedure Search

> {Procedure to search for each value in a linked list pointed by head. If found, cur should point to that node; otherwise, cur should point to the last node in the list. If cur points to the first node, prev should have the null value; otherwise, prev should point to the previous node. }

```
Procedure Search (head, cur, prev: pointer; e: datatype);
begin
  cur := head; {initialization}
  prev := null;
  while (cur^.info != e) and (cur^.link != null)
  do
  begin
    prev := cur;
    cur := cur^.link
  end;
end;
```

# Implementation in C language

Implementation of the above procedure in C language is as follows:

```
struct node
{
  int info;
  struct node * next;
}*start=NULL;
void search()
{
  struct node * curr,*temp;
  int n,flag=0;
  if(start==NULL)
  {
    printf("\n list is empty");
    getch();
    exit(1);
  }

  printf("\n enter the number which you want to search");
```