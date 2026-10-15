Upper bounds are inclusive values in this diagram.

# FIGURE 33-7

# Working with IEnumerable Sources of Data

Parallel.ForEach is also useful to refactor existing ForEach loops that iterate over a collection that exposes an IEnumerable interface.

The simplest definition of the class function Parallel.ForEach, used in Listing 33-8 to generate a new version of the MD5 hashes generation subroutine, ParallelForEachGenerateMD5Hashes, has the following parameters:

+   source — The collection that exposes an IEnumerable interface and provides the data source.
+   body — The delegate to be invoked, once per iteration, and without a predefined execution plan. It receives each element of the source collection — in this case, an Integer.

# LISTING 33-8: A parallelized version of the GenerateMD5Hashes subroutine using Parallel.ForEach with an IEnumerable source

```
Private Function GenerateMD5InputData() As IEnumerable(Of Integer)
    Return Enumerable.Range(1, NUM_AES_KEYS)
End Function
```

![](bbox=[0.125, 0.08, 0.8, 0.58])