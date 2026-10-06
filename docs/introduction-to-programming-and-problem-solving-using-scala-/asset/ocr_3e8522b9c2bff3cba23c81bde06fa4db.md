# Sorting and Searching 405

```
val tmp = a(j)
a(j) = a(min)
a(min) = tmp
}
}
```

As with the standard bubble sort, the outer loop loops $n-1$ times as it has to swap $n-1$ elements into the locations they belong. The contents of the inner loop here are quite short, just a check that changes the $min$ variable. The swap itself is longer than the loop.

The selection sort is not really more efficient than bubble sort in general. However, because the swap is outside of the inner loop, this can be much more efficient in situations where the swaps are expensive. This situation cannot happen for normal Arrays in Scala, but it can be true for *Arrays* in some other languages or if the values being sorted are contained in a file inside the memory of the computer.

# 13.1.3 Insertion Sort

The last sort we will discuss in this section is another one that humans might consider using. It is the INSERTION sort which builds up a sorted group of elements at the beginning of the Array and each new element is inserted into the proper location in that group. The advantage of this sort is that it can do less checking the other one. Once it finds the place to put the element it can stop and move to the next element. It is particularly efficient if the Array is fairly close to sorted, as each element does not have to be moved very far.

The code for insertionSort(a:Array[Double]):Unit is

```
for (j <- 1 until a.length) {
  var i = j-1
  val tmp = a(j)
  while (i >= 0 && a(i) > tmp) {
    a(i+1) = a(i)
    i -= 1
  }
  a(i+1) = tmp
}
```

The outer loop here executes $n-1$ times, but in a different way and for a different reason. Instead of starting at 0 and stopping one sort of the last, this loop starts at 1 and goes to the last element of the *Array*. The reason for this is that an *Array* of one element can be viewed as a sorted *Array*. We take the first element as being where it should be in a group of 1. Then we start with the second element and potentially move it forward if needed.

The code inside the outer loop needs some explaining, as it is a bit different from what we saw with the other sorts. This is the index of the next element that we need to compare to the one we are moving. We also declare a temporary variable called *tmp* that stores the value in the *Array* that we are moving forward. Having the temporary variable prevents us from doing full swaps and makes the code shorter and faster. To understand this, consider again the example of moving cars in a parking lot. Consider you have ten cars, the first