```
}
int count = 0; // Count of non-zero elements

// Traverse the array and if an element is nonzero, then place the element at next available position
for (int i = 0; i < n; i++) {
  if (nums[i] != 0) {
    nums[count++] = nums[i];
  }
}

// Set remaining positions to zero
while (count < n) {
  nums[count++] = 0;
}

std::cout << "Array after pushing zeros to the end:\n";nfor (int num : nums) {
  std::cout << num << " ";
}
```