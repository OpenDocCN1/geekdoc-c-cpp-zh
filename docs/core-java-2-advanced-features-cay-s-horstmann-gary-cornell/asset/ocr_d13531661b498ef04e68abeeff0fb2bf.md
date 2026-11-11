For parallel streams to work well, a number of conditions need to be fulfilled:

+   - The data should be in memory. It would be inefficient to have to wait for the data to arrive.
+   - The stream should be efficiently splittable into subregions. A stream backed by an array or a balanced binary tree works well, but the result of `Stream.iterate` does not.
+   - The stream operations should do a substantial amount of work. If the total work load is not large, it does not make sense to pay for the cost of setting up the parallel computation.
+   - The stream operations should not block.

In other words, don't turn all your streams into parallel streams. Use parallel streams only when you do a substantial amount of sustained computational work on data that is already in memory.

The example program in Listing 1.8 demonstrates how to work with parallel streams.

# Listing 1.8 parallel/ParallelStreams.java

```
```java
package parallel;

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
      String contents = new String(Files.readAllBytes(
         Paths.get("../gutenberg/alice30.txt")), StandardCharsets.UTF_8);
      List<String> wordList = Arrays.asList(contents.split("\\PL+"));

      // Very bad code ahead
      int[] shortWords = new int[10];
      wordList.parallelStream().forEach(s ->
      {
         if (s.length() < 10) shortWords[s.length()]++;
      });
```
```