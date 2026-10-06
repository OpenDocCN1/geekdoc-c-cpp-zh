# Synchronizing Threads

A common requirement for multithreaded applications is that of synchronizing threads. Qt provides the following synchronization classes: QMutex, QReadWriteLock, QSemaphore, and QWaitCondition.

The QMutex class means of protecting a variable or a piece of code so that only one thread can access it at a time. The class provides a lock() function that locks the mutex. If the mutex is unlocked, the current thread seizes it immediately and locks it; otherwise, the current thread is blocked until the thread that holds the mutex unlocks it. Either way, when the call to lock() returns, the current thread holds the mutex until it calls unlock(). QMutex class also provides a tryLock() function that returns immediately if the mutex is already locked.

For example, let's suppose that we wanted to protect the stopped variable of the Thread from the preceding section with QMutex. We would then add the following member variable to Thread:

private:

```
...
QMutex mutex;
};
```

The run() function would change to this:

```
void Thread::run()
{
    forever {
        mutex.lock();
        if (stopped) {
            stopped = false;
            mutex.unlock();
            break;
        }
        mutex.unlock();

        std::cerr << qPrintable(messageStr);
    }
    std::cerr << std::endl;
}
```

The stop() function would become this:

```
void Thread::stop()
```