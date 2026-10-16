I used **notify_one()** rather than **notify_all()** because I only added one element and wanted to keep put() simple. The possibility of multiple consumers and the possibility of consumers falling behind the producer might make me reconsider.

The **get()** is a bit more complicated because it should only block its **thread** if the **mutex** precludes access or if the queue is empty:

```
template<typename T>
void Sync_queue::get(T& val)
{
unique_lock<mutex> lck(mtx);
cond.wait(lck,[this]{ return !q.empty(); });
val=q.front();
q.pop_front();
}
```

A caller of **get()** will remain blocked until the **Sync_queue** is nonempty.
I used a **unique_lock** rather than a plain **lock_guard** because the **lock_guard** is optimized for simplicity and does not offer the operations needed to unlock and relock the **mutex**.
I used **[this]** to enable the lambda to access the **Sync_queue** object (§11.4.3.3).
I return the value from **get()** through a reference argument, rather than as a return value, to be sure that an element type with a copy constructor that can throw will not cause trouble.
That is the conventional technique (e.g., the STL **stack** adaptor provides **pop()** and the containers provide **front()**). Writing a general **get()** that directly returns a value is possible, but surprisingly tricky. For an example, see **future<T>::get()** (§42.4.4).
A simple producer-consumer pair can be very simple:

```
Sync_queue<Message> mq;

void producer()
{
while (true) {
Message m; // ... fill m ... mq.put(m);
}
}
void consumer()
{
while (true) {
Message m; mq.get(m); // ... use m ...
}
}
thread t1 {producer};
thread t2 {consumer};
```

Using a **condition_variable** saves a consumer the bother of explicitly dealing with the case where it runs out of work to do. Had we simply used a **mutex** to control access to the **Sync_queue**, the consumer would have had to repeatedly wake up, look for work on the queue, and decide what to do when it found the queue empty.