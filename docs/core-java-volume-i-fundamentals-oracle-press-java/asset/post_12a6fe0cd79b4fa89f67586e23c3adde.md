
```java
        final int SIZE = 10000000;
        var numbers = new double[SIZE];
        for (int i = 0; i < SIZE; i++) numbers[i] = Math.random();
        var counter = new Counter(numbers, 0, numbers.length, x -> x > 0.5);
        var pool = new ForkJoinPool();
        pool.invoke(counter);
        System.out.println(counter.join());
    }
}

class Counter extends RecursiveTask<Integer>
{
    public static final int THRESHOLD = 1000;
    private double[] values;
    private int from;
    private int to;
    private DoublePredicate filter;

    public Counter(double[] values, int from, int to, DoublePredicate filter)
    {
        this.values = values;
        this.from = from;
        this.to = to;
        this.filter = filter;
    }

    protected Integer compute()
    {
        if (to - from < THRESHOLD)
        {
            int count = 0;
            for (int i = from; i < to; i++)
            {
                if (filter.test(values[i])) count++;
            }
            return count;
51        }
52        else
53        {
54            int mid = from + (to - from) / 2;
55            var first = new Counter(values, from, mid, filter);
56            var second = new Counter(values, mid, to, filter);
57            invokeAll(first, second);
58            return first.join() + second.join();
59        }
60    }
61}
```

## 12.7 Asynchronous Computations

### 12.7.1 Completable Futures

When you have a Future object, you need to call get to obtain the value, blocking until the value is available. The CompletableFuture class implements the Future interface, and it provides a second mechanism for obtaining the result. You register a *callback* that will be invoked (in some thread) with the result once it is available.

```java
CompletableFuture<String> f = ...;
f.thenAccept(s -> Process the result string s);
```

In this way, you can process the result without blocking once it is available.

There are a few API methods that return CompletableFuture objects. For example, you can fetch a web page asynchronously with the HttpClient class that you will encounter in [Chapter 4](#) of Volume II:

```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request =
    HttpRequest.newBuilder(URI.create(urlString)).GET().build();
CompletableFuture<HttpResponse<String>> f = client.sendAsync(
    request, BodyHandlers.ofString());
```

It is nice if there is a method that produces a ready-made `CompletableFuture`, but most of the time, you need to make your own. To run a task asynchronously and obtain a `CompletableFuture`, you don’t submit it directly to an executor service. Instead, you call the static method `CompletableFuture.supplyAsync`. Here is how to read the web page without the benefit of the `HttpClient` class:

```java
public CompletableFuture<String> readPage(URL url)
{
    return CompletableFuture.supplyAsync(() ->
    {
        try
        {
            return new String(url.openStream().readAllBytes(),
        "UTF-8");
        }
        catch (IOException e)
        {
            throw new UncheckedIOException(e);
        }
    }, executor);
}
```

If you omit the executor, the task is run on a default executor (namely the executor returned by `ForkJoinPool.commonPool()`). You usually don’t want to do that.

![](img/0e7b74ef51a065c077b42cd87b362288_1160_0.png)

**CAUTION:**

Note that the first argument of the `supplyAsync` method is a `Supplier<T>`, not a `Callable<T>`. Both interfaces describe functions with no arguments and a return value of type `T`, but a `Supplier` function cannot throw a checked exception. As you can see from the code above, that was not an inspired choice.

A `CompletableFuture` can complete in two ways: either with a result, or with an uncaught exception. In order to handle both cases, use the `whenComplete` method. The supplied function is called with the result (or null if none) and the exception (or null if none).

```java
f.whenComplete((s, t) ->
{
    if (t == null)
    {
        Process the result s;
    }
    else
    {
        Process the Throwable t;
    }
});
```

The `CompletableFuture` is called completable because you can manually set a completion value. (In other concurrency libraries, such an object is called a *promise*.) Of course, when you create a `CompletableFuture` with `supplyAsync`, the completion value is implicitly set when the task has finished. But setting the result explicitly gives you additional flexibility. For example, two tasks can work simultaneously on computing an answer:

```java
var f = new CompletableFuture<Integer>();
executor.execute(() ->
{
    int n = workHard(arg);
    f.complete(n);
});
```

the OK button. That, too, is an event in the future:

```java
public CompletableFuture<URL> getURLInput(String prompt)
```

Here we have two functions `T -> CompletableFuture<U>` and `U -> CompletableFuture<V>`. Clearly, they compose to a function `T -> CompletableFuture<V>` if the second function is called when the first one has completed. That is exactly what `thenCompose` does.

In the preceding section, you saw the `whenComplete` method for handling exceptions. There is also a `handle` method that requires a function processing the result or exception and computing a new result. In many cases, it is simpler to call the `exceptionally` method instead. That method computes a dummy value when an exception occurs:

```java
CompletableFuture<List<URL>> imageURLs = readPage(url)
    .exceptionally(ex -> "<html></html>")
    .thenApply(this::getImageURLs)
```

You can handle a timeout in the same way:

```java
CompletableFuture<List<URL>> imageURLs = readPage(url)
    .completeOnTimeout("<html></html>", 30, TimeUnit.SECONDS)
    .thenApply(this::getImageURLs)
```

Alternatively, you can throw an exception on timeout:

```java
CompletableFuture<String> = readPage(url).orTimeout(30, TimeUnit.SECONDS)
```

The methods in Table 12.3 with void result are normally used at the end of a processing pipeline.

Now let us turn to methods that combine multiple futures (see Table 12.4).

**NOTE:**

Technically speaking, the methods in this section accept parameters of type `CompletionStage`, not `CompletableFuture`. The `CompletionStage` interface describes how to compose asynchronous computations, whereas the `Future` interface focuses on the result of a computation. A `CompletableFuture` is both a `CompletionStage` and a `Future`.

[Listing 12.10](#) shows a complete program that reads a web page, scans it for images, loads the images and saves them locally. Note how all time-consuming methods return a `CompletableFuture`. To kick off the asynchronous computation, we use a little trick. Rather than calling the `readPage` method directly, we make a completed future with the URL argument, and then compose that future with `this::readPage`. That way, the pipeline has a very uniform appearance:

```java
CompletableFuture.completedFuture(url)
    .thenComposeAsync(this::readPage, executor)
    .thenApply(this::getImageURLs)
    .thenCompose(this::getImages)
    .thenAccept(this::saveImages);
```

**Table 12.4** Combining Multiple Composition Objects

| Method | Parameters | Description |
|---|---|---|
| thenCombine | `CompletableFuture<U>, (T, U) -> V` | Execute both and combine the results with the given function. |
| thenAcceptBoth | `CompletableFuture<U>, (T, U) -> void` | Like thenCombine, but with void result. |
| runAfterBoth | `CompletableFuture<?>, Runnable` | Execute the runnable after both complete. |
| applyToEither | `CompletableFuture<T>, T -> V` | When a result is available from one or the other, pass it to the given function. |
| acceptEither | `CompletableFuture<T>, T -> void` | Like applyToEither, but with void result. |
| runAfterEither | `CompletableFuture<?>, Runnable` | Execute the runnable after one or the other completes. |
| static allOf | `CompletableFuture<?>...` | Complete with void result after all given futures complete. |
| static anyOf | `CompletableFuture<?>...` | Complete after any of the given futures completes, yielding its result. |

**Listing 12.10** completableFutures/CompletableFutureDemo.java

```java
 1  package completableFutures;
 2
 3  import java.awt.image.*;
 4  import java.io.*;
 5  import java.net.*;
 6  import java.nio.charset.*;
 7  import java.util.*;
 8  import java.util.concurrent.*;
 9  import java.util.regex.*;
10
11  import javax.imageio.*;
12
```
