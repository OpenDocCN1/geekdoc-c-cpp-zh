```
};
typedef struct Node element;
void main()
{
 element * curr, * head;
 int i;
 head = NULL;
 for(i=1;i<=10;i++)
 {
 curr = (element *)malloc(sizeof(element));
 curr->val = i;
 curr->next = head;
 head = curr;
 }
 curr = head;
 while(curr) {
 printf("%d\n", curr->val);
 curr = curr->next ;
 }
 }
```