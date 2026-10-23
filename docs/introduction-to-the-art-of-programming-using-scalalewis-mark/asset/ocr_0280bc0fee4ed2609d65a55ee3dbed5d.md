array would be extremely inefficient, requiring O(n log(n)) memory. It turns out that we can fairly easily create an array-based version that uses 2n ∈ O(n) memory by making a second array and doing merges from the original array to the second array and back. The following code demonstrates that.

```
def mergeSort[A : Manifest](a:Array[A])(comp:(A,A)=>Int) {
  val data = Array(a,new Array[A](a.length))

  def mergeSortRecur[A](start:Int,end:Int,dest:Int) {
    val src = 1-dest
    if(start==end-1) {
      if(dest==1) data(dest)(start) = data(src)(start)
    } else {
      val mid = (start+end)/2 // Can fail for arrays over 2^30 in length
      mergeSortRecur(start,mid,src)
      mergeSortRecur(mid,end,src)
      var (p1,p2,pdest) = (start,mid,start)
      while(pdest<end) {
        if((p2>=end || comp(data(src)(p1),data(src)(p2))<=0) && p1<mid) {
          data(dest)(pdest) = data(src)(p1)
          p1 += 1
        } else {
          data(dest)(pdest) = data(src)(p2)
          p2 += 1
        }
        pdest += 1
      }
    }
  }

  mergeSortRecur(0,a.length,0)
}
```

Here the first line creates an Array[Array[A]] that holds the original array and our second array which is allocated to be the same size. There is a nested recursive function declared that takes the start and end of the range we are sorting as well as the index of the destination in data. That destination alternates between 0 and 1 as we go down the call stack. The merge is done from src into dest. The initial call uses a destination of 0 so the final sorted version winds up being in the original array.

The comment on the calculation of mid is worth noting. For arrays with a bit more than a billion elements, the quantity start+end can overflow and Int. This will lead to a negative value for mid. You can get around this by using mid = start+(end-start)/2 instead. This expression will work for all legal array sizes.

# 28.4.2 Quicksort

A second sorting example of divide and conquer is the quicksort. Unlike merge sort, the quicksort can be done in-place and, when written that way, it does all of its work going down the stack instead of on the way back up. Unlike merge sort, the quicksort is less stable and can degrade to O(n²) performance. This happens due to poor selection of a pivot. Recall from chapter 15 that a quicksort works by selecting one element to be the “pivot” and then moves elements around so that the pivot is in the correct location. If pivots are selected which belong near the middle of the array, this produces O(n log(n)) performance. However,