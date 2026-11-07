```
```cpp
16        intQueue.enqueue( i );
17        intQueue.printQueue();
18    } // end for

20    int dequeueInteger; // store dequeued integer

22    // dequeue integers from intQueue
23    while ( !intQueue.isQueueEmpty() )
24    {
25        intQueue.dequeue( dequeueInteger );
26        cout << dequeueInteger << " dequeued" << endl;
27        intQueue.printQueue();
28    } // end while

30    Queue< double > doubleQueue; // create Queue of doubles
31    double value = 1.1;

33    cout << "processing a double Queue" << endl;

35    // enqueue floating-point values onto doubleQueue
36    for ( int j = 0; j < 3; ++j )
37    {
38        doubleQueue.enqueue( value );
39        doubleQueue.printQueue();
40        value += 1.1;
41    } // end for

43    double dequeueDouble; // store dequeued double

45    // dequeue floating-point values from doubleQueue
46    while ( !doubleQueue.isQueueEmpty() )
47    {
48        doubleQueue.dequeue( dequeueDouble );
49        cout << dequeueDouble << " dequeued" << endl;
50        doubleQueue.printQueue();
51    } // end while
52 } // end main
```
```

```
```text
processing an integer Queue
The list is: 0
The list is: 0 1
The list is: 0 1 2

0 dequeued
The list is: 1 2

1 dequeued
The list is: 2

2 dequeued
The list is empty
processing a double Queue
The list is: 1.1
```
```

**Fig. 20.17** | Queue-processing program. (Part 2 of 3.)