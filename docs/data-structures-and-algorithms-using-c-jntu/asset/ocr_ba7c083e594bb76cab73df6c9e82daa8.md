```
```cpp
int pos,i;
if(head->flink=NULLL)
{
cout<<"flinked list is empty\n";
return;
}
cout<<"enter the position\n";
cin>>pos;
for(temp1=head,i=0;i<pos;i++,temp1=temp1->flink)
{
temp=temp1;
}
temp->flink=temp1->flink;
temp=temp1->flink;
temp->blink=temp1->blink;
ele=temp1->data;
cout<<"the deleted element is"<<ele<<endl;
free(temp1);
}
template<class t>
void llist<t>::fdisplay()
{
if(head->flink=NULLL)
{
cout<<"flinked list is empty\n";
return;
}
for(temp=head->flink,temp=NULLL;temp=temp->flink)
{
cout<<temp->data<<" ";
}
}
template<class t>
void llist<t>::bdisplay()
{
if(head->flink=NULLL)
{
cout<<"flinked list is empty\n";
return;
}
for(temp=head;temp->flink=NULLL;temp=temp->flink)
{
//cout<<temp->data<<" ";
}
for(temp1=temp;temp1->blink!=NULLL;temp1=temp1->blink)
{
cout<<temp1->data<<" ";
}
}
```
```