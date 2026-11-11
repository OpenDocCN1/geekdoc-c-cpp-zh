```
```java
executors.

/**
 * @version 1.01 2021-05-3013   * @author Cay Horstmann
 */
public class ExecutorDemo
{
   /**
    * Counts occurrences of a given word in a file.
    * @return the number of times the word occurs in the given word
    */
   public static long occurrences(String word, Path path)
   {
      try (var in = new Scanner(path))
      {
         int count = 0;
         while (in.hasNext())
            if (in.next().equals(word)) count++;
         return count;
      }
      catch (IOException ex)
      {
         return 0;
      }
   }

   /**
    * Returns all descendants of a given directory--see Chapters 1 and 2 of Volume II.
    * @param rootDir the root directory
    * @return a set of all descendants of the root directory
    */
   public static Set<Path> descendants(Path rootDir) throws IOException
   {
      try (Stream<Path> entries = Files.walk(rootDir))
      {
         return entries.filter(Files::isRegularFile)
               .collect(Collectors.toSet());
      }
   }
}
```
```