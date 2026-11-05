```
~~~csharp
public async Task MethodA()
{
    await MethodB();
    // Do other work
}

public async Task MethodB()
{
    await MethodC();
    // Do other work
}

public async Task MethodC()
{
    // Or await some other async work
    await Task.Delay(100);
}
~~~
```

This will not perform any better than

```
~~~csharp
public void MethodA()
{
    MethodB();
    // Do other work
}

public void MethodB()
{
    MethodC();
    // Do other work
}

public void MethodC()
{
    Thread.Sleep(100);
}
~~~
```

The primary purpose of async/await is to allow the machine to do additional work - for example, to allow the calling thread to do other work while it's waiting for a result from some I/O operation. In this case, the calling thread is never allowed to do more work than it would have been able to do otherwise, so there's no performance gain over simply calling MethodA(), MethodB(), and MethodC() synchronously.

# ## Section 114.6: Web.config setup to target 4.5 for correct async behaviour

The web.config system.web.httpRuntime must target 4.5 to ensure the thread will reenter the request context before resuming your async method.

```
~~~xml
<httpRuntime targetFramework="4.5" />
~~~
```

Async and await have undefined behavior on ASP.NET prior to 4.5. Async / await will resume on an arbitrary thread that may not have the request context. Applications under load will randomly fail with null reference exceptions accessing the HttpContext after the await. Using HttpContext.Current in WebApi is dangerous because of async

# ## Section 114.7: Simple consecutive calls

```
~~~csharp
public async Task<JobResult> GetDataFromWebAsync()
~~~
```