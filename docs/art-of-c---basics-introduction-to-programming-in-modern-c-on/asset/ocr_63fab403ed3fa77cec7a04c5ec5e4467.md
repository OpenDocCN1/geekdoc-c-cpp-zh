Next, we use the `WhenAll()` method. `WhenAll()` creates a task that will complete when all of the Task objects in the argument have completed. We create a new Task object based on other Tasks (e.g., returned from `StartAsync` calls) and we `await` the new Task to finish, which effectively making the program to `await` until all component tasks to finish.

The `Task` class provides other methods as well which implement different logic.

One important thing to notice here is that the `Server.Run()` method is declared as `async`.

```
public async Task Run() {
    // ...
}
```

You can only use `await` in an `async` method. As stated, you almost always use `await` for async methods, and therefore you can only use, or are most likely to use, async methods in another async method.

This is the case with `async Task Listener.StartAsync()` as well in this example.

Once you start using async APIs, you will end up creating more async methods of your own, and the users of your (public) APIs will end up using more async methods of their own, ... And so on and so on.

Even our (implicit) `Main` method (in the `Program.cs`) is `async`. It calls an async method with `await`.

```
await server.Run();
```

Hence, it must be, and it is, an `async` method. (The compiler generates a version of the `Main()` methods that is compatible with the top-level statements, including the