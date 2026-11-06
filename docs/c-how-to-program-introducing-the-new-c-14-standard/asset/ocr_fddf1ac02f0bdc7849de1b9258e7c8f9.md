# 16.4.12 `min`, `max`, `minmax` and `minmax_element`

**Figure 16.13** demonstrates algorithms `min`, `max`, `minmax` and `minmax_element`.

```
```cpp
// Fig. 16.13: fig16_13.cpp
// Algorithms min, max, minmax and minmax_element.
#include <iostream>
#include <array>
#include <algorithm>
using namespace std;

int main() {
   cout << "The minimum of 12 and 7 is: " << min(12, 7);
   cout << "\nThe maximum of 12 and 7 is: " << max(12, 7);
   cout << "\nThe minimum of 'G' and 'Z' is: " << min('G', 'Z');
   cout << "\nThe maximum of 'G' and 'Z' is: " << max('G', 'Z');

   // determine which argument is the min and which is the max
   auto result1 = minmax({2, 7});
   cout << "\nThe minimum of 12 and 7 is: " << result1.first
      << "\nThe maximum of 12 and 7 is: " << result1.second;

   array<int, 10> items{3, 100, 52, 77, 22, 31, 1, 98, 13, 40};
   ostream_iterator<int> output(cout, " ");
```
```