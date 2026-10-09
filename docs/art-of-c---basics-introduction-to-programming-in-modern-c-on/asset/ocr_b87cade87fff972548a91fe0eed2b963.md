use args, etc.)

Async methods can return values by using a generic version of `Task`. For example, `HttpListener.GetContextAsync()` returns `Task<HttpListenerContext>`. When we call this method with `await`, the "real" return value is of a type `HttpListenerContext`.

For example,

```
var context = await listener.GetContextAsync();
```

The type of `context` is `HttpListenerContext`.

(Or more precisely, a nullable type `HttpListenerContext?` (because we use the implicit `var` declaration), but that is not very significant in this particular context since we, and the compiler, know that `context` is not, and cannot, be null since `GetContextAsync()` returns a non-null `HttpListenerContext` object.)

In this sample code, the `ProcessTextResponse()` method and the `ProcessJsonResponse` method write to the (HTTP) output stream.

Note that they are made `async` using a "trick", e.g., by calling an async method `await Task.Delay(1)`. Otherwise we could have simply created and returned a `Task` object.

In this example, for illustration, we used the async function delegate, `Func<HttpListenerContext, Task>`, although these two particular methods do not take too long to complete.

In general, in the context of Web programming, the handlers may need to do long processing or accessing databases, etc. They `may` take long time to finish, and it is a best practice to use async methods.

# Summary