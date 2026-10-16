```
buffer.deposit(new_item);
}
}
```

```
class Consumer extends Thread {
    private Queue buffer;
    public Consumer(Queue que) {
        buffer = que;
    }
    public void run() {
        int stored_item;
        while (true) {
            stored_item = buffer.fetch();
            //-- Consume the stored_item
        }
    }
}
```

The following code creates a Queue object, and a Producer and a Consumer object, both attached to the Queue object, and starts their execution:

```
Queue buff1 = new Queue(100);
Producer producer1 = new Producer(buff1);
Consumer consumer1 = new Consumer(buff1);
producer1.start();
consumer1.start();
```

We could define one or both of the Producer and the Consumer as implementations of the Runnable interface rather than as subclasses of Thread. The only difference is in the first line, which would now appear as follows:

```
class Producer implements Runnable { . . . }
```

To create and run an object of such a class, it is still necessary to create a Thread object that is connected to the object. This is illustrated in the following code:

```
Producer producer1 = new Producer(buff1);
Thread producerThread = new Thread(producer1);
producerThread.start();
```

Note that the buffer object is passed to the Producer constructor and the Producers object is passed to the Thread constructor.