```
std::string reversed = reverseString(input);
std::cout << "Reversed string: " << reversed << std::endl;

return 0;
}
```

# 143. Develop a recursive function to find the smallest value in an array.

#include <iostream>

```
int findSmallest(int arr[], int n, int index = 0, int smallest = INT_MAX) {
  // Base case: if index is equal to n, return the smallest found so far
  if (index == n) return smallest;

  // If the current element is smaller than the smallest,
  // update the smallest value
  if (arr[index] < smallest) smallest = arr[index];
```