```
```cpp
  for (size_t i{low}; i < items.size() && i <= high; ++i) {
    std::cout << std::format("{: ", items[i]); // display element
  }

  std::cout << "\n";
}

// merge two sorted subarrays into one sorted subarray
template <typename T, size_t size>
void merge(std::array<T, size>& items,
    size_t left, size_t middle1, size_t middle2, size_t right) {
  size_t leftIndex{left}; // index into left subarray
  size_t rightIndex{middle2}; // index into right subarray
  size_t combinedIndex{left}; // index into temporary working array
  std::array<T, size> combined; // working array

  // output two subarrays before merging
  std::cout << "merge:          ";
  displayElements(items, left, middle1);
  std::cout << "               ";
  displayElements(items, middle2, right);
  std::cout << "\n";

  // merge arrays until reaching end of either
  while (leftIndex <= middle1 && rightIndex <= right) {
    // place smaller of two current elements into result
    // and move to next space in array
    if (items[leftIndex] <= items[rightIndex]) {
      combined[combinedIndex++] = items[leftIndex++];
    }
    else {
      combined[combinedIndex++] = items[rightIndex++];
    }
  }

  if (leftIndex == middle2) { // if at end of left array
    while (rightIndex <= right) { // copy in rest of right array
      combined[combinedIndex++] = items[rightIndex++];
    }
  }
  else { // at end of right array
    while (leftIndex <= middle1) { // copy in rest of left array
      combined[combinedIndex++] = items[leftIndex++];
    }
  }

  // copy values back into original array
  for (size_t i = left; i <= right; ++i) {
    items[i] = combined[i];
  }
}
```
```

Fig. 21.5 | Sorting an array into ascending order with merge sort. (Part 2 of 5.)