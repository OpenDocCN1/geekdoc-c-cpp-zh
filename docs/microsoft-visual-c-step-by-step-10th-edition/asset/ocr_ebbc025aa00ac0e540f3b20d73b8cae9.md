```
public void Enqueue(T item) // use 'T' as the type of the method
parameter{
  ...
}
npublic T Dequeue() // use 'T' as the type of the return value
  ...
  T queueItem = this.data[this.tail]; // the data in the array is
of type 'T'
  ...
  return queueItem;
}
```

The type parameter T can be any C# identifier, although the lone character T is commonly used. It is replaced with the type you specify when you create a Queue object. The following examples create a Queue of ints and a Queue of HorseS:

Click here to view code image

```
Queue<int> intQueue = new Queue<int>();
Queue<Horse> horseQueue = new Queue<Horse>();
```

Additionally, the compiler now has enough information to perform strict typing when you build the application. You no longer need to cast data when you call the Dequeue method, the compiler can trap any type mismatch errors early.

Click here to view code image

```
intQueue.Enqueue(99);
int myInt = intQueue.Dequeue(); // no casting necessary
Horse myHorse = intQueue.Dequeue(); // compiler error: cannot implicitly convert type 'int' to 'Horse'
```

You should be aware that this substitution of T for a specified type is not simply a replacement mechanism. Instead, the compiler performs a complete semantic substitution so that you can specify any valid type for T. Here are more examples:

Click here to view code image