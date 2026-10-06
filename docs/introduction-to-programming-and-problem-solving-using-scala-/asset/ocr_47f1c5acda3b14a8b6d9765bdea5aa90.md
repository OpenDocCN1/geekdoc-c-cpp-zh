# Introduction to Programming and Problem-Solving Using Scala

The idea of looking at a location and considering things before or after it based on a sorted order can be used to create fast searching algorithms. The most general of which is the BINARY SEARCH, you keep track of elements that you are considering by two integer indices. We will call them start and end. At any time, you know the value you are looking for, if it is present, it will be an index in the range i ∈ [start,end).⁷ If we are searching the Array, initially start is 0 and end is the length of the Array. We code the midpoint of the range, mid=(start+end)/2, and check if the element at mid is what you are looking for. If it is, we return mid. Otherwise we check if we are looking for greater or less than the element at mid and cut down our range accordingly.

To begin with, we will present an imperative version of this algorithm that uses a while and several declarations.

```
def binarySearch(a:Array[Int], value:Int):Int = {
  var start = 0
  var end = a.length
  var mid = (end+start)/2
  while (end < start && a(mid) != value) {
    if (value < a(mid)) {
      end = mid
    } else {
      start = mid+1
    }
    mid = (end+start)/2
  }
  if (end < start) -1 else mid
}
```

The loop continues as long as the range contains at least one element and the midpoint is not the value we want. Inside the loop, a check is performed to see if the midpoint is less or greater than what we are looking for. If it is less, we set end=mid. This works because end is exclusive, and we have just verified that the element is not at mid. Otherwise we start mid+1. The start is inclusive so we have to move one element beyond the mid. When the loop is completed we return the value of mid or -1 based on whether the element was found or not.

This version of the code is fairly straightforward, but there is a simpler approach. Binary search happens to be algorithmic which lends itself nicely to a recursive implementation. The following code shows what this might look like.

```
def binarySearchRecur(a:Array[Int], value:Int, start:Int, end:Int):Int = {
  if (end < start) -1 else
    val mid = (start+end)/2
    if (a(mid) == value) mid
    else if (value < a(mid)) binarySearchRecur(a, value, start, mid)
    else binarySearchRecur(a, value, mid+1, end)
}
```

Clearly this is shorter than what we had before. Most people would also find this code a bit easier to read than the imperative version. The only drawback is that the function has

> ⁷As a reminder, this notation implies that the range is inclusive for start and exclusive for end.

> ⁸For extremely large arrays this formula for the middle code is problematic as start+end overflow an Int. You could use start+(end-start)/2 instead if that is an issue.