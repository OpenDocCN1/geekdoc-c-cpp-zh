# **Listing 12.7** *(Continued)*

```
```java
51  public static void main(String[] args)
52      throws InterruptedException, ExecutionException, IOException
53  {
54      int processors = Runtime.getRuntime().availableProcessors();
55      ExecutorService executor = Executors.newFixedThreadPool(processors);
56      Path pathToRoot = Path.of(".");
57      for (Path p : descendants(pathToRoot))
58      {
59          if (p.getFileName().toString().endsWith(".java"))
60              executor.execute(() -> process(p));
61      }
62      executor.shutdown();
63      executor.awaitTermination(10, TimeUnit.MINUTES);
64      map.forEach((k, v) ->
65      {
66          if (v >= 10)
67              System.out.println(k + " occurs " + v + " times");
68      });
69  }
70 }
```
```

# ### 12.5.4 Bulk Operations on Concurrent Hash Maps

The Java API provides bulk operations on concurrent hash maps that can safely execute even while other threads operate on the map. The bulk operations traverse the map and operate on the elements they find as they go along. No effort is made to freeze a snapshot of the map in time. Unless you happen to know that the map is not being modified while a bulk operation runs, you should treat its result as an approximation of the map’s state.

There are three kinds of operations:

+   - `search` applies a function to each key and/or value, until the function yields a non-null result. Then the search terminates and the function’s result is returned.
+   - `reduce` combines all keys and/or values, using a provided accumulation function.
+   - `forEach` applies a function to all keys and/or values.

Each operation has four versions:

+   - *operationKeys*: operates on keys.
+   - *operationValues*: operates on values.