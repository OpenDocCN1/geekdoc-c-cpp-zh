```
```java
class MyThread extends Thread{

    public void run()
    { ... }
}

...

Thread t = new MyThread();

...
```
```

or by defining a class that implements the **Runnable** interface (which only requires the definition of a run method), and then passing an object of this class to the **Thread** constructor:

```
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
```

This latter mechanism is more versatile, so we use it in our examples.

Defining a thread does not begin executing it. Instead, a thread begins running when the **start** method is called:

```
```java
t.start(); // now t will execute the run method
```
```

The **start** method in turn will call run. Although one could call the run method directly, this will in general not work, since the system must perform some internal bookkeeping before calling run. Note also that every Java program already is executing inside a thread whose run method is main. Thus, when a new thread’s execution is begun by calling start, the main program will still continue to execute to completion in its own thread (in other words, the start method of a thread immediately returns, while the thread itself continues to execute). However, the entire *program* will not finish execution until all of its threads complete the execution of their run methods.