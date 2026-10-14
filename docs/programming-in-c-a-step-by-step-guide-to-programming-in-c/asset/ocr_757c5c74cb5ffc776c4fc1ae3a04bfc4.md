```
printf("The queue is full can not insert a value\n");
exit(0);
}
queue[*rear] = value;
}
void delete(int queue[], int *front, int rear, int * value)
{
if(*front == rear)
{
printf("The queue is empty can not delete a value\n");
exit(0);
}
*front = (*front + 1) % MAX; *value = queue[*front]; }
void main()
{
int queue[MAX];
int front,rear;
int n,value;
front=0; rear=0;
do
{
do
{
```