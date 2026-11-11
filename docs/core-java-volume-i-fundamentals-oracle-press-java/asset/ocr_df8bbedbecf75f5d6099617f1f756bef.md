# NOTE:

Technically speaking, the methods in this section accept parameters of type `CompletionStage`, not `CompletableFuture`. The `CompletionStage` interface describes how to compose asynchronous computations, whereas the `Future` interface focuses on the result of a computation. A `CompletableFuture` is both a `CompletionStage` and a `Future`.

[Listing 12.10](#) shows a complete program that reads a web page, scans it for images, loads the images and saves them locally. Note how all time-consuming methods return a `CompletableFuture`. To kick off the asynchronous computation, we use a little trick. Rather than calling the `readPage` method directly, we make a completed future with the URL argument, and then compose that future with `this::readPage`. That way, the pipeline has a very uniform appearance:

```
```java
CompletableFuture.completedFuture(url)
    .thenComposeAsync(this::readPage, executor)
    .thenApply(this::getImageURLs)
    .thenCompose(this::getImages)
    .thenAccept(this::saveImages);
```
```

**Table 12.4** Combining Multiple Composition Objects