involve one or more reader threads accessing some shared data and one or many writer threads modifying the data. For example:

```
MyData data;
ReadWriteLock lock;
```

```
void ReaderThread::run()
{
  ...
  lock.lockForRead();
  access_data_without_modifying_it(&data);
  lock.unlock();
  ...
}
```

```
void WriterThread::run()
{
  ...
  lock.lockForWrite();
  modify_data(&data);
  lock.unlock();
  ...
}
```

For convenience, we can use the QReadLock and QWriteLock classes to lock and unlock a QReadWriteLock.

QSemaphore is another generalization of mutexes, but unlike read-write locks, semaphores can be used to guard a certain number of identical resources. The following two code snippets show the correspondence between QSemaphore and QMutex:

```
QSemaphore semaphore(1);
semaphor.acquire();
semaphor.release();
```

```
QMutex mutex;
mutex.lock();
mutex.unlock();
```

By passing 1 to the constructor, we tell the semaphore that it controls a single resource. The advantage of using a semaphore is that we can pass numbers other than 1 to the constructor and then call acquire() multiple times to acquire many resources.