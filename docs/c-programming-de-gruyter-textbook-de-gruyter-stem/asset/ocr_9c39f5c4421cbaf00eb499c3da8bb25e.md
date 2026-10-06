# 388 - 9 Collections and Their Organization

```
template <class T>
T Queue<T>::Delete(void) //Delete the queue head, return its
               //value(Dequeue)
{
    T temp;
    if (count == 0) //Terminate the program if queue is empty
    {
        std::cerr << "Deleting from an empty queue!" << endl;
        exit(1);
    }
    temp = qlist[front]; //Save the value of queue head
    count--; //Decrease the number of elements
    front = (front+1) % MaxSize; //Increase the pointer of queue head
                               //by 1, implement circular queue by
                               //reminder
    return temp; //Return the value of queue head
}
```

```
template <class T>
T Queue<T>::Front(void) const //Return the value of queue head
{ return qlist[front]; }
```

```
template <class T>
int Queue<T>::Length(void) const //Return the number of elements
{ return count; }
```

```
template <class T>
int Queue<T>::IsEmpty(void) const //Check whether the queue is empty
{ return count == 0; } //Return the boolean value of count ==0
```

```
template <class T>
int Queue<T>::Full(void) const //Check whether the queue is full
{ return count == MaxSize; } //Return the boolean value of count == MaxSize
```

```
template <class T>
void Queue<T>::Queue(void) //Clear the queue
{
    count = 0;
    front = 0;
    rear = 0;
}
```