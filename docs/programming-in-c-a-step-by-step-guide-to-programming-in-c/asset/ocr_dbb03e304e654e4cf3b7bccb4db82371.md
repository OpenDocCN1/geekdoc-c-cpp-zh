```
```c
struct node *temp;
temp = p;
printf("The data values in the list are\n");
if(p!= NULL)
{
    do
    {
        printf("%d\t",temp->data);
        temp=temp->link;
    } while (temp!= p);
}
else
    printf("The list is empty\n");

void main()
{
    int n;
    int x;
    struct node *start = NULL;
    printf("Enter the nodes to be created \n");
    scanf("%d",&n);
    while ( n -- > 0)
    {
```
```