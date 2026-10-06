# Threads, Concurrent Execution, and Synchronization 135

# Example 166 Producers and Consumers Communicating via a Monitor

A buffer has room for integer, and a method Put for storing into the buffer (if empty) and a method Get for reading from the buffer (if non-empty); it is a monitor (section 21.2). A thread calling Get must obtain the lock on the buffer. If it finds that the buffer is empty, it calls Wait to release the lock and wait until something has been put into the buffer. If another thread calls Put and Pulse, then the getting thread will start competing for the buffer lock again, and if it gets it, will continue executing.

```
class Buffer {
    private int contents;
    private bool empty = true;
    public int get() {
        lock (this);
        while (empty) Monitor.Wait(this);
        empty = true;
        Monitor.Pulse(this);
        return contents;
    }
    public void Put(int v) {
        lock (this);
        while (!empty) Monitor.Wait(this);
        empty = false; contents = v;
        Monitor.Pulse(this);
    }
}
```

# Example 167 Deadlock

Careless locking of more than one object can cause deadlock. Assume that there are one left shoe and one right shoe (two objects) and two people (threads) want to use them. First one person, the pair of shoes. But if two shoes are created by new Person("groucho", left, right) and new Person("harpo", right, left), then the first person may lock the left shoe, and the second person may lock the right one, and then both wait forever for the other shoe. This is avoided by always locking the objects in the same fixed order (instance, before right).

```
class Person {
    String name, fst, snd;
    public Person(String name, String fst, String snd) {
        this.name = name; this.fst = fst; this.snd = snd;
        new Thread(new ThreadStart(Run)).Start();
    }
    public void Run() {
        lock (this);
        Console.WriteLine(name + " got " + fst);
        Thread.Sleep(0); // Yields to other threads
        lock (snd) { Console.WriteLine(name + " got " + snd);
            Console.WriteLine(name + " released " + snd);
        }
        Console.WriteLine(name + " released " + fst);
    }
}}
```