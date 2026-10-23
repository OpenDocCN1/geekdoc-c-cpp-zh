```
```scala
var flip=true
var j=0
while(flip && j<a.length-1) {
  flip=false
  for(i <- 0 until a.length-1-j) {
    if(a(i) > a(i+1)) {
      val tmp=a(i)
      a(i)=a(i+1)
      a(i+1)=tmp
      flip=true
    }
  }
  j+=1
}
```
```

This code adds a few more lines to deal with the flag and the fact that we have to do the counting ourselves with a while loop. The flag is called `flip` and it starts off as true. However, before the inner loop starts it is always set to false and only get set back to true when a swap is done.

# 13.1.2 Selection Sort (Min/Max)

The next sort we want to consider is one that humans are far more likely to employ, especially in a situation like sorting the cars where moving cars around takes a significant amount of effort. The sort is the SELECTION SORT and it is called this because it runs through the values and selects one and places it where it belongs. In order for this to work you have to know where the value should go. This is easy if the value is either the largest or the smallest in the collection. As such, the selection sort is typically implemented as either a minimum sort (MIN SORT) or a maximum sort (MAX SORT). In theory one can also write a min-max sort that picks both and moves them to where they belong.

We will write a min sort here. It is fairly trivial to convert this to a max sort. The inner loop of the min sort will run through all of the currently unsorted collection and find the minimum element in that. If that element is not already where it should be, it is swapped into place. For an Array, the fact that this is a swap is significant. To understand this, think about the cars. Shifting all the cars over one is hard. Swapping two is much easier. The Array is like the parking lot with fixed locations. Certain other data structures could act more similar to file folders which slide around easily and might allow shifting. If you use an Array and a shift instead of a swap, the code you produce will be both longer and significantly slower.

```
```scala
def minSort(a:Array[Double]) {
  for(j <- 0 until a.length-1) {
    var min=j
    for(i <- j+1 until a.length) {
      if(a(i) < a(min)) min=i
    }
    if(min!=j) {
      val tmp=a(j)
      a(j)=a(min)
      a(min)=tmp
    }
  }
}
```
```