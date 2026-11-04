The output is shown here:

```
~~~
Length of nums is 300
~~~
```

As the output verifies, Length obtains the number of elements that nums can hold, which is 300 (10×5×6) in this case. It is not possible to use Length to obtain the length of a specific dimension.

The inclusion of the Length property simplifies many algorithms by making certain types of array operations easier—and safer—to perform. For example, the following program uses Length to reverse the contents of an array by copying it back-to-front into another array:

```
~~~csharp
// Reverse an array.

using System;

class RevCopy {
  static void Main() {
    int i, j;
    int[] nums1 = new int[10];
    int[] nums2 = new int[10];

    for(i=0; i < nums1.Length; i++) nums1[i] = i;

    Console.Write("Original contents: ");
    for(i=0; i < nums2.Length; i++)
      Console.Write(nums1[i] + " ");

    Console.WriteLine();

    // Reverse copy nums1 to nums2.
    if(nums2.Length >= nums1.Length) // make sure nums2 is long enough
      for(i=0, j=nums1.Length-1; i < nums1.Length; i++, j--)
        nums2[j] = nums1[i];

    Console.Write("Reversed contents: ");
    for(i=0; i < nums2.Length; i++)
      Console.Write(nums2[i] + " ");

    Console.WriteLine();
  }
}
~~~
```

Here is the output:

```
~~~
Original contents: 0 1 2 3 4 5 6 7 8 9
Reversed contents: 9 8 7 6 5 4 3 2 1 0
~~~
```

Here, Length helps perform two important functions. First, it is used to confirm that the target array is large enough to hold the contents of the source array. Second, it provides the termination condition of the for loop that performs the reverse copy. Of course, in this simple example, the size of the arrays is easily known, but this same approach can be applied to a wide range of more challenging situations.