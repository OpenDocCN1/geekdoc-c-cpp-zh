```
int main()
{
int opt;
while(1)
{
cout<<"\n 1. INSERT 2. DELETE 0. EXIT";
cin>>opt;
if(opt==1)
{
insert();
cout<<"\n AFTER INSERTION THE QUEUE IS :";
display();
}
else
if(opt==2)
{
delete();
printf("\n AFTER DELETE THE QUEUE IS :");
display();
}
else
if(opt==0)
exit(0);
}
}
```

# 7.9.4 Program for Linked Stack

```
#include<stdio.h>
#include<dos.h>
struct stack
{
int info;
struct stack *next;
};
struct stack *start=NULL,*node, *first,*New;
void push()
{
New = (struct stack *)malloc(sizeof(struct stack));
printf("\n Enter a number");
scanf("%d",&New->info);
if(start == NULL)
{
start = New;
New->next = NULL;
}
```