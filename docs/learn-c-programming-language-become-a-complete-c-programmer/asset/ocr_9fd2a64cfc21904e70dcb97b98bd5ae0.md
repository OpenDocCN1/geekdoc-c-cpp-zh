I used **duration_cast** to adjust the clock’s units to the nanoseconds I wanted. See §5.4.1 and §35.2 before trying anything more complicated than this with time. The time facilities are found in `<chrono>`.

The basic support for communicating using external events is provided by **condition_variables** found in `<condition_variable>` (§42.3.4). A **condition_variable** is a mechanism allowing one **thread** to wait for another. In particular, it allows a **thread** to wait for some *condition* (often called an *event*) to occur as the result of work done by other **thread**s.

Consider the classical example of two **threads** communicating by passing messages through a **queue**. For simplicity, I declare the **queue** and the mechanism for avoiding race conditions on that **queue** global to the producer and consumer:

```
class Message { // object to be communicated
// ...
};

queue<Message> mqueue; // the queue of messages
condition_variable mcond; // the variable communicating events mutex mmutex; // the locking mechanism
```

The types **queue**, **condition_variable**, and **mutex** are provided by the standard library.
The **consumer()** reads and processes **Messages**:

```
void consumer()
{
while(true) {
unique_lock<mutex> lck{mmutex}; // acquire mmutex while (mcond.wait(lck)) /* do nothing*/; // release lck and wait;

// re-acquire lck upon wakeup // get the message auto m = mqueue.front();

mqueue.pop();
lck.unlock(); // release lck
// ... process m ...
}
}
```

Here, I explicitly protect the operations on the **queue** and on the **condition_variable** with a **unique_lock** on the **mutex**. Waiting on **condition_variable** releases its lock argument until the wait is over (so that the queue is non-empty) and then reacquires it.

The corresponding **producer** looks like this:

```
void producer()
{
while(true) {
Message m;
// ... fill the message ...
unique_lock<mutex> lck {mmutex}; // protect operations
```