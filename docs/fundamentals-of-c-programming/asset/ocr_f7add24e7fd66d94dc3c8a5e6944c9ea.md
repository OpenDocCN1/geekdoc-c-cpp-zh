```
int main() {
  // Make a vector of integers
  std::vector<int> vec = { 23, -3, 10, 4, 215, 0, -3, 2 };

  auto working = vec; // Make a copy to keep the original unchanged
  std::cout << "Before: " << " " << working << '\n';
  std::sort(std::begin(working), std::end(working), less_than<int>());
  std::cout << "Ascending: " << " " << working << '\n';
  std::cout << '\n';
  working = vec; // Restore the original sequence
  std::cout << "Before: " << " " << working << '\n';
  std::sort(std::begin(working), std::end(working), greater_than<int>());
  std::cout << "Descending: " << " " << working << '\n';
  std::cout << '\n';
  working = vec; // Restore the original sequence
  std::cout << "Before: " << " " << working << '\n';
  std::sort(std::begin(working), std::end(working),
            [](int a, int b) { return a > b; });
  std::cout << "Descending: " << " " << working << '\n';
  std::cout << '\n';
  working = vec; // Restore the original sequence
  std::cout << "Before: " << " " << working << '\n';
  std::sort(std::begin(working), std::end(working));
  std::cout << "Ascending: " << " " << working << '\n';
}
```

The following shows the results of Listing 20.26 (stdsort.cpp) sorting activity:

| Label | Values |
|---|---|
| Before: | (23, -3, 10, 0, 4, 215, 0, -3, 2) |
| Ascending: | {-3, -3, 0, 2, 4, 10, 10, 23, 215} |
| Before: | (23, -3, 10, 4, 215, 0, -3, 2) |
| Descending: | {215, 23, 10, 4, 2, 0, -3, -3} |
| Before: | (23, -3, 10, 0, 4, 215, 0, -3, 2) |
| Descending: | {215, 23, 10, 4, 2, 0, -3, -3} |
| Before: | (23, -3, 10, 4, 215, 0, -3, 2) |
| Ascending: | {-3, -3, 0, 2, 4, 10, 10, 23, 215} |

The last call to std::sort in Listing 20.26 (stdsort.cpp) uses the overload that does not supply a comparator function. The default comparison operation in this case uses operator< to compare the elements for proper ordering, and thus it sorts in non-descending (ascending) order.

The comparison function, if present, must accept two arguments of the same type that the container holds. The function must return a Boolean result. The function should return true if the first argument must appear before the second argument in a sorted sequence. The function should return false if the first argument should not appear before the second argument in a sorted sequence.

std::copy: The std::copy function copies the elements from one container to another. The following code copies the contents of vector v1 to vector v2:

```
std::vector<int> v1 { 10, 20, 30, 40 };
```