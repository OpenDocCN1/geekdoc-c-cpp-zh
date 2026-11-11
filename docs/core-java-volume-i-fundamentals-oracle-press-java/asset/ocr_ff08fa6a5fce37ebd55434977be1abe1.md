```
```java
98     */
99     public static void search(Path file, String keyword) throws
       IOException
100    {
101        try (var in = new Scanner(file, StandardCharsets.UTF_8))
102        {
103            int lineNumber = 0;
104            while (in.hasNextLine())
105            {
106                lineNumber++;
107                String line = in.nextLine();
108                if (line.contains(keyword))
109                    System.out.printf("%s:%d:%s%n", file,
110                    lineNumber, line);
111            }
112        }
113    }
```
```

# java.util.concurrent.ArrayBlockingQueue<E> 5

+   - `ArrayBlockingQueue(int capacity)`
+   - `ArrayBlockingQueue(int capacity, boolean fair)`

constructs a blocking queue with the given capacity and fairness settings. The queue is implemented as a circular array.

# java.util.concurrent.LinkedBlockingQueue<E> 5
java.util.concurrent.LinkedBlockingDeque<E> 6

+   - `LinkedBlockingQueue()`
+   - `LinkedBlockingDeque()`