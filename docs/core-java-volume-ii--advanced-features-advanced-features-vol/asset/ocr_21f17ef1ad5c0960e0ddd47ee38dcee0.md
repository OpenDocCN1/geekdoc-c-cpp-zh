**NOTE:** By default, parallel streams use the global fork-join pool returned by `ForkJoinPool.commonPool()`. That is fine if your operations don’t block and you don’t share the pool with other tasks. There is a trick to substitute a different pool. Place your operations inside the `submit` method of a custom pool.

```
ForkJoinPool customPool = ...;
result = customPool.submit(() ->
    stream.parallel().map(...).collect(...)).get();

Or, asynchronously:

CompletableFuture.supplyAsync(() ->
    stream.parallel().map(...).collect(...),
    customPool).thenAccept(result -> ...);
```

**NOTE:** If you want to parallelize stream computations based on random numbers, don’t start out with a stream obtained from the `Random.ints`, `Random.longs`, or `Random.doubles` methods. Those streams don’t split. Instead, use the `ints`, `longs`, or `doubles` methods of the `SplittableRandom` class.

The example program in Listing 1.8 demonstrates how to work with parallel streams.

# **Listing 1.8** `parallel/ParallelStreams.java`

```
package parallel;

/**
 * @version 1.01 2018-05-01
 * @author Cay Horstmann
 */

import static java.util.stream.Collectors.*;

import java.io.*;
import java.nio.charset.*;
import java.nio.file.*;
import java.util.*;
import java.util.stream.*;

public class ParallelStreams
{
    public static void main(String[] args) throws IOException
    {
        // Continues
```