```
}
temp->flink=temp1->flink;
temp1->flink=temp;
temp->data=ele;
temp->blink=temp1;
temp1->blink=temp;
temp=blink=temp;
}
template<class t>
void llist<t>::deletef()
{
	t ele;
if(head->flink=NULLL)
{
	cout<<"flinked list is empty\n";
	return;
}
temp=head->flink;
temp1->temp->flink;
head->flink=temp1;
temp1->blink=head;
ele->temp->data;
free(temp);
cout<<"the deleted element is"<<ele<<endl;
}
template<class t>
void llist<t>::deletee()
{
	t ele;
if(head->flink=NULLL)
{
	cout<<"flinked list is empty\n";
	return;
}
for(temp1=head,temp1->flink!=NULLL,temp1=temp1->flink)
{
	temp=temp1;
}
temp->flink=NULLL;
ele=temp1->data;
temp->ele=data;
free(temp1);
cout<<"the deleted element is"<<ele<<endl;
}
template<class t>
void llist<t>::deletea()
{
	t ele;
```