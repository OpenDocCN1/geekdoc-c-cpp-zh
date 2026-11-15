Output 4.9 shows the results of Listing 4.15.

# Output 4.9:

```
104
```

The program begins by passing the first command-line argument to DirectoryCountLines(), or by using the current directory if no argument was provided. This method first iterates through all the files in the current directory and totals the source code lines for each file. After each file in the directory, the code processes each subdirectory by passing the subdirectory back into the DirectoryCountLines() method, rerunning the method using the subdirectory. The same process is repeated recursively through each subdirectory until no more directories remain to process.

Readers unfamiliar with recursion may find it cumbersome at first. Regardless, it is often the simplest pattern to code, especially with hierarchical type data such as the filesystem. However, although it may be the most readable, it is generally not the fastest implementation. If performance becomes an issue, developers should seek an alternative solution in place of a recursive implementation. The choice generally hinges on balancing readability with performance.

# BEGINNER TOPIC

# Infinite Recursion Error

A common programming error in recursive method implementations appears in the form of a stack overflow during program execution. This usually happens because of infinite recursion, in which the method continually calls back on itself, never reaching a point that indicates the end of the recursion. It is a good practice for programmers to review any method that uses recursion and verify that the recursion calls are finite.

A common pattern for recursion using pseudocode is as follows:

```
M(x)
{
    if x is trivial
```