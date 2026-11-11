# 12.4.2 Windows (cl.exe)

# 12.4.2.1 Exclusive Locking

```
C:\Users\rainer>exclusiveLockingTelebook.exe

teleBook.size(): 88799
Process time: 0.121072 seconds

C:\Users\rainer>
```

The initial telephone book

# 12.4.2.2 Shared Locking

```
C:\Users\rainer>sharedLockingTelebook.exe

teleBook.size(): 88799
Process time: 0.217009 seconds

C:\Users\rainer>
```

The initial telephone book

Honestly, the Windows numbers surprised me because shared locking is on Windows two times slower than exclusive locking. It seems that the usage of a std::shared_lock and a std::lock_guard together with a std::shared_time_mutex is a heavyweight operation so that sharing does not pay off.

# 12.5 Avoidance of Loopholes

Don't pass the internals of your data structure to clients. Internals can be passed by reference or pointer to the outside world. Passing an arbitrary callable to the data structure opens a loophole, which is difficult challenging to spot.