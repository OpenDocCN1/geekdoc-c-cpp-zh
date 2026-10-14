```
struct node *pop(struct node *p, int *value) {
struct node *temp;
if(p==NULL)
{

printf(" The stack is empty can not pop Error\n"); exit(0);
}
*value = p->data;
temp = p;
p = p->link;
free(temp);
return(p);
}

void main()
{
struct node *top = NULL;
int n,value;
do
{
do
{
printf("Enter the element to be pushed\n"); scanf("%d",&value);
top = push(top,value);
```