```
server.put(move(job1)); server.put(move(job2)); server.put(move(job3));
auto r1 = f1.get();
auto r2 = f2.get();
auto r3 = f3.get();
```

The server **thread** would take the **packaged_tasks** from the **server** queue and execute them in some suitable order. Typically, the tasks would carry data with them from the calling context.

The tasks are written essentially like ordinary functions, function objects, and lambdas. The server calls the tasks essentially like ordinary (callback) functions. The **packaged_tasks** are actually easier for the server to use than ordinary functions because the handling of their exceptions has been taken care of.

# 42.4.4 **future**

A **future** is a handle to a shared state (§42.4.1). It is where a task can retrieve a result deposited by a **promise** (§42.4.2).

```
future fu {};
future fu {fu2};
fu.~future() fu=move(fu2) future<T> (§iso.30.6.6) (continues)
```

+   - Default constructor: no shared state; noexcept
+   - Move constructor: **fu** gets **fu2**’s shared state, if any; **fu2** no longer has a shared state; noexcept
+   - Destructor: release the shared state, if any
+   - Move assignment: **fu** gets **fu2**’s shared state, if any; **fu2** no longer has a shared state; release **fu**’s old shared state, if any

```
sf=fu.share() x=fu.get()

fu.get()
fu.valid()
fu.wait()
fs=fu.wait_for(d)

fs=fu.wait_until(tp) future<T>
```

**(continued) (§iso.30.6.6)**

Move **fu**’s value into a **shared_future sf**; **fu** no longer has a shared state; **fu**’s value is moved into **x**; if an exception was stored in **fu**, throw it; **fu** no longer has a shared state; don’t try to **get()** twice

For **future<void>**: like x=fu.get(), but don’t move any value. Is **fu** valid? that is, does **fu** have a shared state? noexcept
Block until a value arrives
Block until a value arrives or for a **duration d**;
**fs** tells if a value is **ready**, a **timeout** occurred, or execution was **deferred**. Block until a value arrives or until a **time_point tp**;
**fs** tells if a value is **ready**, a **timeout** occurred, or execution was **deferred**