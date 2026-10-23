```
//moving to the right position
while(i<pos)
{
prev=current;
current=current->next;
i++;
}//end of while
if(prev==NULL)
{
newnode->next=first;
first=newnode;
end->next=first;
return;
} //end of inner if
newnode->next=current;
prev->next=newnode;
}  //end of out if
else
cout<<"List size less than position, try again..\n";
}//end of function insert_beg
//search function
int list::search(int el)
{
int found=0;
node *current=first;
int i=0,cnt;
cnt=count();
while(i<=cnt)
{
if(current->data==el)
{
found=1;
break;
}
current=current->next;
```