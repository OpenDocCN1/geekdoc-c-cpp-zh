# ### 21.5.1 Implementation

Figure 21.3 uses the simple but inefficient insertion sort algorithm to sort a 10-element array's values into ascending order. Function template `insertionSort` (lines 8–24) implements the algorithm.

```
~~~cpp
// Fig. 20.3: InsertionSort.cpp
// Sorting an array into ascending order with insertion sort.
#include <array>
#include <format>
#include <iostream>

// sort an array into ascending order
template <typename T, size_t size>
void insertionSort(std::array<T, size>& items) {
  // loop over the elements of the array
  for (size_t next{1}; next < items.size(); ++next) {
    T insert{items[next]}; // save value of next item to insert
    size_t moveIndex{next}; // initialize location to place element

    // search for the location in which to put the current element
    while ((moveIndex > 0) && (items[moveIndex - 1] > insert)) {
      // shift element one slot to the right
      items[moveIndex] = items[moveIndex - 1];
      --moveIndex;
    }

    items[moveIndex] = insert; // place insert item back into array
  }
}

int main() {
  std::array<int, 10> data{34, 56, 4, 10, 77, 51, 93, 30, 5, 52};

  std::cout << "Unsorted array:\n";

  // output original array
  for (size_t i{0}; i < data.size(); ++i) {
    std::cout << std::format("{:>4}", data[i]);
  }

  insertionSort(data); // sort the array

  std::cout << "\nSorted array:\n";

  // output sorted array
  for (size_t i{0}; i < data.size(); ++i) {
    std::cout << std::format("{:>4}", data[i]);
  }

  std::cout << "\n";
}
~~~
```

**Fig. 21.3 |** Sorting an array into ascending order with insertion sort. (Part 1 of 2.)