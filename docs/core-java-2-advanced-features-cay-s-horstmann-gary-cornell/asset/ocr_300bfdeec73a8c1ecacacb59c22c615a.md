can then optimize the computation, for example by using multiple threads for computing sums and counts and combining the results.

In this chapter, you will learn how to use the Java stream library, which was introduced in Java SE 8, to process collections in a “what, not how” style.

# ### 1.1 From Iterating to Stream Operations

When you process a collection, you usually iterate over its elements and do some work with each of them. For example, suppose we want to count all long words in a book. First, let’s put them into a list:

```
```java
String contents = new String(Files.readAllBytes(
        Paths.get("alice.txt")), StandardCharsets.UTF_8); // Read file into string
List<String> words = Arrays.asList(contents.split("\\PL+"));
        // Split into words; nonletters are delimiters
```
```

Now we are ready to iterate:

```
```java
long count = 0;
for (String w : words)
{
    if (w.length() > 12) count++;
}
```
```

With streams, the same operation looks like this:

```
```java
long count = words.stream()
    .filter(w -> w.length() > 12)
    .count();
```
```

The stream version is easier to read than the loop because you do not have to scan the code for evidence of filtering and counting. The method names tell you right away what the code intends to do. Moreover, while the loop prescribes the order of operations in complete detail, a stream is able to schedule the operations any way it wants, as long as the result is correct.

Simply changing stream into parallelStream allows the stream library to do the filtering and counting in parallel.

```
```java
long count = words.parallelStream()
    .filter(w -> w.length() > 12)
    .count();
```
```