```
int n;
double sum = 0.0; // Use double to handle possible fractional results

// Prompt the user for the size of the array
std::cout << "Enter the number of elements: ";
std::cin >> n;

// Allocate memory for the array
int* arr = new int[n];

// Prompt the user for the array elements
std::cout << "Enter " << n << " integers:" << std::endl;
for (int i = 0; i < n; i++) {
  std::cin >> arr[i];
}

// Calculate the sum of the elements
for (int i = 0; i < n; i++) {
  sum += arr[i];
}

// Calculate the average
```