```
printf("Enter the element : ");
scanf("%d",&m);
printf("Enter the position after which this element i
inserted : ");
scanf("%d",&position);
addafter(m,position);
break;
case 4:
if(start==NULL)
{
printf("List is empty\n");
continue;
}
printf("Enter the element for deletion : ");
scanf("%d",&m);
del(m);
break;
case 5:
display();
break;
case 6:
printf("Enter the element to be searched : ");
scanf("%d",&m);
search(m);
break;
case 7:
exit();
default:
printf("Wrong choice\n");
}//End of switch*/
/*End of while*/
/*End of main()*/

create_list(int data)
{
struct node *q,*tmp;
tmp=malloc(sizeof(struct node));
tmp->info=data;
tmp->link=NULL;
if(start==NULL) /*If list is empty*/
start=tmp;
else
{
/*Element inserted at the end*/
q=start;
while(q->link!=NULL)
q=q->link;
q->link=tmp;
}
/*End of create_list()*/
```