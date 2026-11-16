```
```c
void displayMenu()
{
 printf("\n Representation of Linear Queue using Arrays ...");
 printf("\n\t 1. Enqueue ");
 printf("\n\t 2. Dequeue ");
 printf("\n\t 3. Peek ");
 printf("\n\t 4. Size ");
 printf("\n\t 5. View ");
 printf("\n\t 6. Exit ");
}
int isEmpty()
{
 extern int queue[], front, rear;
 if(front == -1 && rear == -1)
 /* Check for Empty Queue */
 return 1;
 else
 return 0;
}
int isFull()
{
 extern int queue[], front, rear;
 if(rear == (QSIZE - 1))
 /* Check for Occupied Queue */
 return 1;
 else
 return 0;
}
int enqueue(int value)
{
 extern int queue[], front, rear;
 if(isFull())
 /* Check for Rear at last position */
 return -1;
 else if(isEmpty())
 /* Check for Empty Queue */
 front = rear = 0;
 else
 rear = rear + 1;
 queue[rear] = value;
 return 0;
}
int dequeue(int *value)
{
 extern int queue[], front, rear;
```
```