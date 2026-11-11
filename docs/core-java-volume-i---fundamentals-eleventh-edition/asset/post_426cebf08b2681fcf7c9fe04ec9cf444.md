
Finally, the static allOf and anyOf methods take a variable number of completable futures and yield a CompletableFuture<Void> that completes when all of them, or any one of them, completes. The allOf method does not yield a result. The anyOf method does not terminate the remaining tasks.

**Table 12.4 Combining Multiple Composition Objects**

| Method | Parameters | Description |
|---|---|---|
| thenCombine | CompletableFuture<U>, (T, U) -> V | Execute both and combine the results with the given function. |
| thenAcceptBoth | CompletableFuture<U>, (T, U) -> void | Like thenCombine, but with void result. |
| runAfterBoth | CompletableFuture<?>, Runnable | Execute the runnable after both complete. |
| applyToEither | CompletableFuture<T>, T -> V | When a result is available from one or the other, pass it to the given function. |
| acceptEither | CompletableFuture<T>, T -> void | Like applyToEither, but with void result. |
| runAfterEither | CompletableFuture<?>, Runnable | Execute the runnable after one or the other completes. |
| static allOf | CompletableFuture<?>... | Complete with void result after all given futures complete. |
| static anyOf | CompletableFuture<?>... | Complete after any of the given futures completes, yielding its result. |

> **NOTE:** Technically speaking, the methods in this section accept parameters of type CompletionStage, not CompletableFuture. The CompletionStage interface describes how to compose asynchronous computations, whereas the Future interface focuses on the result of a computation. A CompletableFuture is both a CompletionStage and a Future.

Listing 12.10 shows a complete program that reads a web page, scans it for images, loads the images and saves them locally. Note how all time-consuming methods return a CompletableFuture. To kick off the asynchronous computation, we use a little trick. Rather than calling the readPage method directly, we make a completed future with the URL argument, and then compose that future with this::readPage. That way, the pipeline has a very uniform appearance:

```java
CompletableFuture.completedFuture(url)
    .thenComposeAsync(this::readPage, executor)
    .thenApply(this::getImageURLs)
    .thenCompose(this::getImages)
    .thenAccept(this::saveImages);
```

### Listing 12.10 completableFutures/CompletableFutureDemo.java

```java
1 package completableFutures;
2
3 import java.awt.image.*;
4 import java.io.*;
5 import java.net.*;
6 import java.nio.charset.*;
7 import java.util.*;
8 import java.util.concurrent.*;
9 import java.util.regex.*;
10
11 import javax.imageio.*;
12
13 public class CompletableFutureDemo
14 {
15   private static final Pattern IMG_PATTERN = Pattern.compile(
16     "<i?[!?]?[Mm][Gg][^>]*?[\\s]+[Ss][Rr][Cc][\\s]*=[\\s]*[\"']?([^\"'>]+)[\"']?[^>]*>");
17   private ExecutorService executor = Executors.newCachedThreadPool();
18   private URL urlToProcess;
19
20   public CompletableFuture<String> readPage(URL url)
21   {
22     return CompletableFuture.supplyAsync(() ->
23     {
24       try
25       {
26         var contents = new String(url.openStream().readAllBytes(),
27           StandardCharsets.UTF_8);
28         System.out.println("Read page from " + url);
29         return contents;
30       }
31       catch (IOException e)
32       {
33         throw new UncheckedIOException(e);
34       }
35     }, executor);
36   }
37
38   public List<URL> getImageURLs(String webpage) // not time-consuming
39   {
try
{
    var result = new ArrayList<URL>();
    Matcher matcher = IMG_PATTERN.matcher(webpage);
    while (matcher.find())
    {
        var url = new URL(urlToProcess, matcher.group(1));
        result.add(url);
    }
    System.out.println("Found URLs: " + result);
    return result;
}
catch (IOException e)
{
    throw new UncheckedIOException(e);
}
}

public CompletableFuture<List<BufferedImage>> getImages(List<URL> urls)
{
    return CompletableFuture.supplyAsync(() ->
    {
        try
        {
            var result = new ArrayList<BufferedImage>();
            for (URL url : urls)
            {
                result.add(ImageIO.read(url));
                System.out.println("Loaded " + url);
            }
            return result;
        }
        catch (IOException e)
        {
            throw new UncheckedIOException(e);
        }
    }, executor);
}

public void saveImages(List<BufferedImage> images)
{
    System.out.println("Saving " + images.size() + " images");
    try
    {
        for (int i = 0; i < images.size(); i++)
        {
```

For example, if you want to read a file when the user clicks a button, don't do this:

```java
var open = new JButton("Open");
open.addActionListener(event ->
   { // BAD--long-running action is executed on UI thread
      var in = new Scanner(file);
      while (in.hasNextLine())
      {
         String line = in.nextLine();
         . . .
      }
   });
```

Instead, do the work in a separate thread.

```java
open.addActionListener(event ->
   { // GOOD--long-running action in separate thread
      Runnable task = () ->
      {
         var in = new Scanner(file);
         while (in.hasNextLine())
         {
            String line = in.nextLine();
            . . .
         }
      };
      executor.execute(task);
   });
```

However, you cannot directly update the user interface from the worker thread that executes the long-running task. User interfaces such as Swing, JavaFX, or Android are not thread-safe. You cannot manipulate user interface elements from multiple threads, or they risk becoming corrupted. In fact, JavaFX and Android check for this, and throw an exception if you try to access the user interface from a thread other than the UI thread.

Therefore, you need to schedule any UI updates to happen on the UI thread. Each user interface library provides some mechanism to schedule a Runnable for execution on the UI thread. For example, in Swing, you call

```java
EventQueue.invokeLater(() -> label.setText(percentage + "% complete"));
```

It is tedious to implement user feedback in a worker thread, so each user interface library provides some kind of helper class for managing the details, such as SwingWorker in Swing, Task in JavaFX, and AsyncTask in Android. You specify actions for the long-running task (which is run on a separate thread), as well as progress updates and the final disposition (which are run on the UI thread).

Whenever you want to do some work in the worker thread, construct a new worker. (Each worker object is meant to be used only once.) Then call the execute method. You will typically call execute on the event dispatch thread, but that is not a requirement.

It is assumed that a worker produces a result of some kind; therefore, `SwingWorker<T, V>` implements `Future<T>`. This result can be obtained by the get method of the Future interface. Since the get method blocks until the result is available, you don’t want to call it immediately after calling execute. It is a good idea to call it only when you know that the worker has been completed. Typically, you call get from the done method. (There is no requirement to call get. Sometimes, processing the progress data is all you need.)

Both the intermediate progress data and the final result can have arbitrary types. The `SwingWorker` class has these types as type parameters. A `SwingWorker<T, V>` produces a result of type T and progress data of type V.

To cancel the work in progress, use the cancel method of the Future interface. When the work is canceled, the get method throws a CancellationException.

As already mentioned, the worker thread’s call to publish will cause calls to process on the event dispatch thread. For efficiency, the results of several calls to publish may be batched up in a single call to process. The process method receives a `List<V>` containing all intermediate results.

Let us put this mechanism to work for reading in a text file. As it turns out, a `JTextArea` is quite slow. Appending lines from a long text file (such as all lines in *The Count of Monte Cristo*) takes considerable time.

To show the user that progress is being made, we want to display the number of lines read in a status line. Thus, the progress data consist of the current line number and the current line of text. We package these into a trivial inner class:

```java
private class ProgressData
{
    public int number;
    public String line;
}
```

The final result is the text that has been read into a StringBuilder. Thus, we need a `SwingWorker<StringBuilder, ProgressData>`.

In the doInBackground method, we read a file, a line at a time. After each line, we call publish to publish the line number and the text of the current line.

```java
@Override public StringBuilder doInBackground() throws IOException, InterruptedException
{
    int lineNumber = 0;
```
