```
...
private object[] data;
...
public Queue()
{
    this.data = new object[DEFAULTQUEUESIZE];
}

public Queue(int size)
{
    this.data = new object[size];
    ...
}

public void Enqueue(object item)
{
    ...
}

public object Dequeue()
{
    ...
    object queueItem = this.data[this.tail];
    return queueItem;
}
```

Remember that you can use the object type to refer to a value or variable of any type. All reference types automatically inherit (either directly or indirectly) from the System.Object class in Microsoft .NET. (In C#, object is an alias for System.Object.) Now, because the Enqueue and Dequeue methods manipulate objects, you can operate on queues of any Circle objects, Horse objects, Whale objects, or objects on any of the classes that you have seen in this book. However, you must cast the value returned by the Dequeue method to the appropriate type because the compiler will not perform the conversion from the object type automatically.

Click here to view code image

```
Queue queue = new Queue();
Horse myHorse = new Horse();
queue.Enqueue(myHorse); // Now legal - Horse is an object
...
```