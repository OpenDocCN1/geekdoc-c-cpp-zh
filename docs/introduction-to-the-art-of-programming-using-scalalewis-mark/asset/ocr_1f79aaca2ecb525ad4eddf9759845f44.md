very little work compared to the smaller gaps because they do not contain many elements, but once you get to the smaller gaps the data is mostly sorted so you get close to the best-case performance of the insertion sort. The sort always ends with a gap size of 1, which is doing a normal insertion sort, so you know that the result is fully sorted.

The only trick to the Shell sort is figuring out what to do about the gap. The initial suggestion was to start at half the size of the Array and decrease it by factors of 2. This often works well, but spacings that are factors of 2 apart will keep even and odd subsets separate until you get down to a gap of 1 and in certain cases that can actually lead to $O(n^2)$ behavior. For this reason, we use a slightly different factor.

```
```scala
def shellSort(a:Array[Double]) {
  var gap=a.length/2
  while(gap>=1) {
    for(j <- gap until a.length) {
      var i=j-gap
      val tmp=a(j)
      while(i>=0 && a(i)>tmp) {
        a(i+gap) = a(i)
        i -= gap
        renderSort(a)
      }
      a(i+gap) = tmp
      renderSort(a)
    }
    gap=(gap/2.2).round.toInt
  }
}
```
```

This code was created by defining the var gap and writing the while loop, then cutting and pasting the insertion sort inside of the while loop. Once there, all the places where i was incremented or decremented by 1 were changed so the 1 was gap. The factor of 2.2 gives better spacings though you do need to round and convert back to an Int. Two calls to renderSort were left in this code so that you can easily visualize it. Of the sorts we have discussed so far, this one is probably the most important to visualize to get a grasp on what it is doing and why the process of reducing the gap is significant.

The exact order of the Shell sort is harder to pin down. This is largely because it varies with the selection of gap scaling and can range from $O(n^2)$ at the poor end all the way to $O(n\log^2 n)$ at the good end. Reasonable implementations like the one shown here will tend to give $O(n^{3/2})$ performance. This might not seem like a tremendous improvement, but if $n$ gets large, the difference can be quite dramatic.

# 13.2 Searching

While sorting data is something that we do a fair bit with computers, searching for data is a far more common task. A lot of the things that you do with computers on a regular basis involve searching for information either just to retrieve it or to modify information related to what is found. This makes sense, as running through data is something that computers do particularly quickly and efficiently.