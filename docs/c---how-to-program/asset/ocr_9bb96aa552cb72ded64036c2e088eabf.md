```
```c
 displayElements(array, SIZE); // print the array
}

// function that merge sorts the array
void mergeSort(int array[], size_t length)
{
   sortSubArray(array, 0, length - 1);
}

// function that sorts a piece of the array
void sortSubArray(int array[], size_t low, size_t high)
{
   // test base case: size of array is 1
   if ((high - low) >= 1) { // if not base case...
      size_t middle1 = (low + high) / 2;
      size_t middle2 = middle1 + 1;

      // output split step
      printf("%s", "split:   ");
      displaySubArray(array, low, high);
      printf("%s", "       ");
      displaySubArray(array, low, middle1);
      printf("%s", "       ");
      displaySubArray(array, middle2, high);
      puts("\n");

      // split array in half and sort each half recursively
      sortSubArray(array, low, middle1); // first half
      sortSubArray(array, middle2, high); // second half

      // merge the two sorted arrays
      merge(array, low, middle1, middle2, high);
   }
}

// merge two sorted subarrays into one sorted subarray
void merge(int array[], size_t left, size_t middle1,
   size_t middle2, size_t right)
{
   size_t leftIndex = left; // index into left subarray
   size_t rightIndex = middle2; // index into right subarray
   size_t combinedIndex = left; // index into temporary array
   int tempArray[SIZE]; // temporary array

   // output two subarrays before merging
   printf("%s", "merge:   ");
   displaySubArray(array, left, middle1);
   printf("%s", "       ");
   displaySubArray(array, middle2, right);
   puts("\n");
}
```
```

Fig. D.3  |  The merge sort algorithm. (Part 2 of 5.)