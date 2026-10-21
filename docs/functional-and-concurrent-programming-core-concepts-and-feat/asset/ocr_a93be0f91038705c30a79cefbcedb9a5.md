```
val queue = ArrayBlockingQueue[Option[String]](capacity)

def searchFile(path: Path): Unit =
  Using.resource(Source.fromFile(path.toFile)(UTF8)) { in =>
    for line <- in.getLines() do if isMatch(line) then queue.put(Some(line))
  }

val searchTask: Runnable = () =>
  var file = Option(files.poll())
  while file.nonEmpty do
    searchFile(file.get)
    file = Option(files.poll())
  queue.put(None)

val writeTask: Runnable = () =>
  var active = N
  while active > 0 || !queue.isEmpty do
    queue.take() match
      case None => active -= 1
      case Some(line) =>
        out.write(line)
        out.write('\n')
```

Listing 23.9: Searching files and storing results as a producer–consumer pattern.

The queue of matching lines is changed into a queue of options: Some(line) represents a match, and None is the poison pill. Each searching task inserts a single None in the queue at the end of its search. The file writing task counts these None values and knows to terminate when all have been received and the queue is empty. Counting is internal to the task and does not entail the use of a thread-safe atomic integer. Indeed, producers and consumers coordinate entirely through the queue and rely on no other shared synchronization mechanism. (The total number of producing tasks, N does need to be known by the consumer, though.)

# 23.6 Summary

+   - The Java standard library offers a flexible implementation of exclusive locks through class ReentrantLock, which can be used as an alternative to intrinsic locks. It provides users with the same basic locking properties but defines additional methods for threads to be interrupted or to time out (or even not block at all) when a lock is not available.

+   - The library also defines non-exclusive locks, commonly known as read-write locks. These locks can be acquired in shared mode or in exclusive mode; that is, a