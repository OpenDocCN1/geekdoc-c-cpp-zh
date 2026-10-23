As with the standard bubble sort, the outer loop happens n − 1 times as it has to swap n − 1 elements into the locations they belong. The contents of the inner loop here are quite short, just a check that changes the min variable if needed. The swap itself is longer than the loop.

The selection sort is not really more efficient than the bubble sort in general. However, because the swap is outside of the inner loop, this sort can be much more efficient in those situations where the swaps are expensive. This situation can not happen for normal Arrays in Scala, but it can be true for Arrays in some other languages or if the values being sorted are contained in a file instead of the memory of the computer.

# 13.1.3 Insertion Sort

The last sort we will discuss in this section is another one that humans might consider using. It is called the INSERTION SORT because the way it works is to build up a sorted group of elements at the beginning of the Array and each new element is inserted into the proper location in that group. The advantage of this sort is that it can do less checking. Once it finds the place to put the element it can stop and move to the next element. It is particularly efficient if the Array is fairly close to sorted as each element typically does not have to be moved very far.

The code for an insertion sort can be written in the following way.

```
def insertionSort(a:Array[Double]) {
  for(j <- 1 until a.length) {
    var i=j-1
    val tmp=a(j)
    while(i>=0 && a(i)>tmp) {
      a(i+1) = a(i)
      i -= 1
    }
    a(i+1) = tmp
  }
}
```

The outer loop here still executes n − 1 times, but in a different way and for a different reason. Instead of starting at 0 and stopping one short of the last element, this loop starts at 1 and goes to the last element of the Array. The reason for this is that an Array of one element can be viewed as a sorted Array. So we take the first element as being where it should be in a group of 1. Then we start with the second element and potentially move it forward if needed.

The code inside the outer loop can use some explaining as well, as this is a bit different from what we saw with the other two sorts. It begins with the declaration of the variable i, which begins at j-1. This is the index of the next element that we need to compare to the one we are moving. We also declare a temporary variable called tmp that stores the value in the Array that we are moving forward. Having the temporary variable here prevents us from doing full swaps and makes the code both shorter and faster. To understand this, consider again the example of moving cars in a parking lot. Consider you have ten cars, the first eight of which are already sorted. You need to move the ninth one forward to the place it belongs, potentially several spots down. You would not do this by swapping cars one after the other. Instead, you would pull that car out and put it in the one empty spot to the side. Then you would move the sorted cars down, one at a time, until you had cleared