
# Solutions to Chapter 18 | Threads and Locks

18.1 What's the difference between a thread and a process?

# SOLUTION

Processes and threads are related to each other but are fundamentally different.

A process can be thought of as an instance of a program in execution. Each process is an independent entity to which system resources (CPU time, memory, etc.) are allocated and each process is executed in a separate address space. One process cannot access the variables and data structures of another process. If you wish to access another process's resources, such as pipes, files, sockets etc., inter-process communications have to be used such.

A thread uses the same stack space of a process. A process can have multiple threads. A key difference between processes and threads is that multiple threads share parts of their state. Typically, one allows multiple threads to read and write the same memory (no processes can directly access the memory of another process). However, each thread still has its own registers and own stack, but other threads can read and write the memory.

A thread is a particular execution path of a process; when one thread modifies a process resource, the change is immediately visible to sibling threads.

![](img/50974dc108b2978cf2cacf9397df9934_264_0.png)

# Solutions to Chapter 18 | Threads and Locks

18.3 Implement a singleton design pattern as a template such that, for any class Foo, you can call Singleton::instance() and get a pointer to an instance of a singleton of type Foo. Assume the existence of a class Lock which has acquire() and release() methods. How could you make your implementation thread safe and exception safe?

# SOLUTION

```cpp
using namespace std;
/* Place holder for thread synchronization lock */
class Lock {
public:
    Lock() { /* placeholder code to create the lock */ }
    ~Lock() { /* placeholder code to deallocate the lock */ }
    void AcquireLock() { /* placeholder code to acquire the lock */ }
    void ReleaseLock() { /* placeholder to release the lock */ }
};

/* Singleton class with a method that creates a new instance of the
   class of the type of the passed in template if it does not
already exist. */
template <class T> class Singleton {
private:
    static Lock lock;
    static T* object;
protected:
    Singleton() { }
public:
    static T* instance();
};
Lock Singleton::lock;
T* Singleton::Instance() {
    /* if object is not initialized, acquire lock */
    if (object == nullptr) {
        lock.AcquireLock();
        /* If two threads simultaneously check and pass the first "if"
           condition, then the only one who acquired the lock first
           should create the instance */
        if (object == nullptr) {
            object = new T;
        }
        lock.ReleaseLock();
    }
    return object;
}
```

![](img/50974dc108b2978cf2cacf9397df9934_265_0.png)

# Solutions to Chapter 18 | Threads and Locks

```cpp
int main() {
    /* foo is any class defined for which we want singleton access */
    Foo* singleton_foo = Singleton<Foo>::Instance();
    return 0;
}
```

The general method to make a program thread safe is to lock shared resources whenever write permission is given. This way, if one thread is modifying the resource, other threads can not modify it.

# Solutions to Chapter 18 | Threads and Locks

18.4 Design a class which provides a lock only if there are no possible deadlocks.

# SOLUTION

For our solution, we implement a wait / die deadlock prevention scheme.

```java
class MyThread extends Thread {
    long time;
    ArrayList<Resource> res = new ArrayList<Resource>();
    public ArrayList<Resource> getRes() { return res; }

    public void run() {
        /* Run infinitely */
        time = System.currentTimeMillis();
        int count = 0;
        while (true) {
            if (count < 4) {
                if (Question.acquireResource(this, Question.r[count])) {
                    res.add(Question.r[count]);
                    count++;
                    System.out.println("Resource: [" + Question.r[count].getId() + "] acquired by thread: [" + this.getName() + "]");
                    try {
                        sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            } else {
                this.stop();
            }
        }
    }

    public long getTime() { return time; }
    public void setRes(ArrayList<Resource> res) { this.res = res; }
    MyThread(String name) {
        super(name);
    }
}
```

# Solutions to Chapter 18 | Threads and Locks

18.5 Suppose we have the following code:

```cpp
class Foo {
public:
    A(....); /* If A is called, a new thread will be created and
    * the corresponding function will be executed. */
    B(....); /* same as above */
    C(....); /* same as above */
}
Foo f;
f.A(....);
f.B(....);
```

iii) Suppose we have the following code:
```cpp
class Foo {
public:
    A(....); /* If A is called, a new thread will be created and
    * the corresponding function will be executed. */
    B(....); /* same as above */
    C(....); /* same as above */
}
Foo f;
f.A(....);
f.B(....);
```

i) Can you design a mechanism to make sure that B is executed after A?
We are given a class with synchronized A, and normal method C. If you have two threads in one instance of a program, can they call A at the same time?
Not possible; read the above paragraph.

ii) Can you design a mechanism to make sure that all the methods will be executed in sequence?
We are given a class with synchronized A, and normal method C. If you have two threads in one instance of a program, can they call A and C at the same time?
Yes. Only methods of the same object which are declared with the keyword synchronized can't be interleaved.

# Solutions to Chapter 18 | Threads and Locks

18.6 You are given a class with synchronized A, and normal method C. If you have two threads in one instance of a program, can they call A at the same time? Can they call A and C the same time?

# SOLUTION

Java provides two ways to achieve synchronization: synchronized method and synchronized statement.

Synchronized method: Methods of a class which need to be synchronized are declared with "synchronized".

```java
public class Synchronized {
    // Variables
    public synchronized Method1() {
        // Statements
    }
    public synchronized method2() {
        // Statements
    }
}
```

Synchronized statement: It provides the synchronization for a group of statements rather than a method as a whole. It needs to provide the object on which these statements will be applied, unlike in a synchronized method.

Syntax: synchronized statements on "this" object

```java
synchronized(this) {
    /* statement 1
    ...
    * statement N */
}
```

# Solutions to Chapter 19 | Moderate

19.1 Write a function to swap a number in place without temporary variables.

# SOLUTION

This is a classic interview problem. If you haven't heard this problem before, you can approach it by taking the difference between a and b:

```java
public static void swap(int a, int b) {
    a = b - a; // 9 - 5 = 4
    b = b - a; // 9 - 4 = 5
    a = a + b; // 4 + 5 = 9

    System.out.println("a: " + a);
    System.out.println("b: " + b);
}
```

You can then optimize it as follows:

```java
public static void swap_opt(int a, int b) {
    a = a^b;
    b = a^b;
    a = a^b;

    System.out.println("a: " + a);
    System.out.println("b: " + b);
}
```
