

```java
class MyThread extends Thread{

    public void run()
    { ... }
}

...

Thread t = new MyThread();

...
```

或通过定义一个实现 **Runnable** 接口的类（它只需要定义 run 方法），然后将该类的对象传递给 **Thread** 构造函数：

```java
class MyRunner implements Runnable{

    public void run()
    { ... }
}

...

MyRunner m = new MyRunner();
Thread t = new Thread(m);

...
```

后一种机制更通用，因此我们在示例中使用它。

定义线程并不会开始执行它。相反，线程在调用 **start** 方法时开始运行：

```java
t.start(); // now t will execute the run method
```

**start** 方法进而会调用 run。虽然可以直接调用 run 方法，但通常这样做不会奏效，因为系统必须在调用 run 之前执行一些内部簿记工作。还请注意，每个 Java 程序都已在某个线程中执行，其 run 方法是 main。因此，当通过调用 start 开始新线程的执行时，主程序仍将在其自己的线程中继续执行到完成（换句话说，线程的 start 方法会立即返回，而线程本身继续执行）。然而，整个 *程序* 要到所有线程完成其 run 方法的执行后才会结束执行。

线程是如何被销毁的？正如我们刚才所说，最简单的机制是让每个线程执行完其 run 方法，到那时它将无需程序员干预而自行消失。线程也可以通过在线程对象上调用 join 方法来等待其他线程完成后再继续：

```java
Thread t = new Thread(m);
t.start(); // t begins to execute
// do some other work
t.join(); // wait for t to finish
// continue with work that depends on t being finished
```

因此，Java 线程表现出前面定义的 fork-join 并行性（fork 操作由 start 方法给出）。

另一种等待线程完成执行的方法是使用 interrupt 方法中断它：

```java
Thread t = new Thread(m);
t.start(); // t begins to execute
// do some other work
t.interrupt(); // tell t that we are waiting for it
t.join(); // continue to wait
// continue
```

interrupt 方法，如这段代码所示，并不会真正停止被中断线程的执行，而只是设置线程对象中的一个内部标志，该标志可由对象用来测试是否有其他线程调用了其 interrupt 方法。这允许线程在真正退出前继续执行一些清理代码。interrupt 方法的语义有些复杂，因此我们暂时推迟更完整的讨论。

请注意，当调用 t.join() 时，当前线程（即发出此调用的线程）会被阻塞，并且只有在 t 退出其 run 方法后才会解除阻塞。如果 t 也处于阻塞状态等待某个事件，则可能导致死锁。如果存在死锁的真实可能性，那么我们可以通过只等待指定时间然后超时来避免它：

```java
t.join(1000); // wait 1 second for t, then give up
```

通常，任何使当前线程阻塞的 Java 方法，例如 join，都有如上所示的超时版本，因为 Java 运行时系统不会尝试发现或防止死锁。确保不会发生死锁完全取决于程序员。

到目前为止，我们尚未讨论如何在 Java 中强制共享数据的互斥。即使仅使用迄今为止描述的机制，Java 线程也很有用，事实上并行矩阵乘法已经可以编写（参见练习 13.17），因为不需要互斥。

通常，Java 线程会共享一些内存或其他资源，通常是通过将要共享的对象传递给用于创建线程的 Runnable 对象的构造函数。⁸ 例如，假设有多个不同的线程使用共享队列添加和删除对象：

⁸也可以创建内部 Runnable 类并通过非局部访问共享数据。

```java
class Queue{
    ...
    public Object dequeue(){
        if (empty()) throw EmptyQueueException ;
        ...
    }
    public void enqueue(Object obj) { ... }
    ...
}

class Remover implements Runnable{
    public Remover(Queue q){ ... }
    public void run(){ ... q.dequeue() ... }
    ...
}

class Inserter implements Runnable{
    public Inserter(Queue q){ ... }
    public void run(){ ... q.enqueue(...) ... }
    ...
}

Queue q = new Queue(...);
...
Remover r = new Remover(q);
Inserter i = new Inserter(q);
Thread t1 = new Thread(r);
Thread t2 = new Thread(i);
t1.start();
t2.start();
...
```

现在队列 q 在线程 t1 和 t2 之间共享，并且需要在 q 内部确保互斥的机制是必要的，这样就不会出现一个线程执行 q.dequeue() 而另一个线程执行 q.enqueue() 的情况。在 Java 中，这是通过在 Queue 类的定义中使用 synchronized 关键字⁹来实现的：

> ⁹在本文中，我们只讨论方法同步。事实上，在 Java 中，任何代码块都可以对存在局部引用的任何对象进行同步（同步方法隐式地对当前对象 this 进行同步）。方法同步是块同步的特例；例如，上面的 enqueue 方法可以通过以下等效代码进行同步：public void enqueue(Object obj) { synchronized(this) { ... } }。

```java
class Queue{
    ...
    synchronized public Object dequeue(){
        if (empty()) throw EmptyQueueException;
        ...
    }

    synchronized public void enqueue(Object obj){ ... }
    ...
}
```

在 Java 中，每个对象都有一个单一的 **lock**（参见第 13.4 节）供线程使用。当线程尝试执行对象的同步方法时，它必须首先获取该对象的锁。如果锁被另一个线程持有，它会等待锁可用，获取它，然后继续执行同步方法。退出方法后，它在继续自己的执行之前释放锁。¹⁰因此，两个线程不能同时执行同一对象的任何同步方法。（未同步的方法不受影响。）这解决了前述的互斥问题。

在考虑扩展示例之前，我们在此讨论 Java 中的一个额外线程机制：如何使线程等待某些显式条件然后恢复执行。例如，假设在前面的队列示例中，我们知道如果调用 dequeue，则最终会存在一个对象供调用线程从队列中移除。那么，在空队列上生成异常是不希望的——线程应简单地等待对象出现在队列中。

如果条件可以在同步方法的代码中进行测试，执行该方法的线程可以通过调用对象的 **wait()** 方法手动挂起（**wait** 是类 **Object** 的方法，因此每个对象都有此方法）。一旦线程等待某个条件，它还需要由另一个线程手动重新唤醒（通常是建立所需条件的线程）。这是使用对象的 **notify()** 或 **notifyAll()** 方法完成的。请注意，Java 中的每个对象都有一个等待列表，其中包含所有在该对象上调用过 **wait** 的线程，按未指定的顺序排列。**notify()** 方法只会唤醒该列表中的一个（任意）线程，而 **notifyAll()** 会唤醒列表中的所有线程。通常优先使用 **notifyAll()** 而不是 **notify()**，因为无法预测 **notify()** 会唤醒哪个线程，而等待列表中的线程可能正在等待与刚刚建立的条件不同的条件。

现在让我们重新考虑上面的队列示例。与其在空队列上生成异常，dequeue 方法应调用 **wait**，而 enqueue 操作应调用 **notifyAll**，因为它使队列非空：

