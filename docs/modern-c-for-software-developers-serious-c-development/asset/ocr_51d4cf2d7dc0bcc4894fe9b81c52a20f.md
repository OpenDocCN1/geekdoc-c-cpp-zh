that we do not need to create an instance of a class in order to invoke a static member function.

Lastly, we can execute a functor in a thread. A functor is an object that behaves like a function. This behaviour is induced by overloading the () operator.

# Thread Joins

Trying to join a thread that does not exist or joining the same thread more than once will throw an exception:

```
t1.join();              // exception thrown
nt1.join();
```

To prevent these types of errors we should test that a thread is joinable before joining the thread:

```
if (t1.joinable()) t1.join();
```

# Detaching A Thread From It's Parent Thread

A thread t1 can be detached with:

```
t1.detach();
```

This statement will cause the parent and child thread to execute independently from one another. A join stops the execution of the parent thread until the child thread has finished execution. The child thread does not have to be joined to the parent thread before detaching it.

After a thread is created we must join or detach it.