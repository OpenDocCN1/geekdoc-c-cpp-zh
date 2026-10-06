```
{
private:
    int front, rear, count; //Pointer of queue head and tail,
    //number of elements
    T qlist[MaxSize]; //Array of elements of queue

public:
    Queue(void); //Constructor, initialize queue head,
                 //tail and number of elements
    void QInsert(const T& item); //Enqueue new element
    T QDequeue(void); //Dequeue element
    void ClearQueue(void); //Clear the queue

    T QFront(); //Get the element of queue head

    //Test the status of queue
    int QLength(void) const; //Get the length of the queue
                             //(number of elements)
    int QEmpty(void) const; //Check whether queue is empty
    int QFull(void) const; //Check whether queue is full
}
```

//Constructor, initialize queue head, tail and number of elements
template<class T>
Queue<T>::Queue(void) : front(0), rear(0), count(0)
{}

```
template<class T>
void Queue<T>::QInsert(const T& item)
{//Insert element to the queue tail(enqueue)
{
    if (count == MaxSize)//Terminate the program if queue is full
    {
        std::cerr << "Queue overflow!" << std::endl;
        exit(1);
    }
    count++; //Increase the number of elements
    qlist[rear] = item; //Insert the element to queue tail
    rear = (rear+1) % MaxSize; //Increase the pointer of queue tail
                 //by 1, implement circular queue by
                 //reminder
}
```