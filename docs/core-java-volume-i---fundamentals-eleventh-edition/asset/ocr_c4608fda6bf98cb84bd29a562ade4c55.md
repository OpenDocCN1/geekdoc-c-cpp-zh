# ### 12.7.1 Completable Futures

When you have a future object, you need to call `get` to obtain the value, blocking until the value is available. The `CompletableFuture` class implements the `Future` interface, and it provides a second mechanism for obtaining the result. You register a `callback` that will be invoked (in some thread) with the result once it is available.

```
```java
CompletableFuture<String> f = ...;
f.thenAccept(s -> Process the result string s);
```
```

In this way, you can process the result without blocking once it is available. There are a few API methods that return `CompletableFuture` objects. For example, you can fetch a web page asynchronously with the experimental `HttpClient` class that you will encounter in Chapter 4 of Volume II:

```
```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder(URI.create(urlString)).GET().build();
CompletableFuture<HttpResponse<String>> f = client.sendAsync(
      request, BodyHandler.asString());
```
```

It is nice if there is a method that produces a ready-made `CompletableFuture`, but most of the time, you need to make your own. To run a task asynchronously and obtain a `CompletableFuture`, you don't submit it directly to an executor service. Instead, you call the static method `CompletableFuture.supplyAsync`. Here is how to read the web page without the benefit of the `HttpClient` class:

```
```java
public CompletableFuture<String> readPage(URL url)
{
   return CompletableFuture.supplyAsync(() ->
      {
         try
         {
            return new String(url.openStream().readAllBytes(), "UTF-8");
         }
         catch (IOException e)
         {
            throw new UncheckedIOException(e);
         }
      }, executor);
}
```
```

If you omit the executor, the task is run on a default executor (namely the executor returned by `ForkJoinPool.commonPool()`). You usually don't want to do that.