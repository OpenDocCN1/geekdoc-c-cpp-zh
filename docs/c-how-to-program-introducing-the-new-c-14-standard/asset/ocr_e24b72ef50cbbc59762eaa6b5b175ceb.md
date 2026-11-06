| 3 | 30 | 300 | 3000 |
|---|---|---|---|
| 4 | 40 | 400 | 4000 |
| 5 | 50 | 500 | 5000 |

9. 4.19 **(Find the Two Largest Numbers)** Using an approach similar to that in **Exercise 4.17**, find the *two* largest values among the 10 numbers. [**Note:** You must input each number only once.]

10. 4.20 **(Validating User Input)** The examination-results program of Fig. 4.14 assumes that any value input by the user that’s not a 1 must be a 2. Modify the application to validate its inputs. On any input, if the value entered is other than 1 or 2, keep looping until the user enters a correct value.

11. 4.21 **(What Does this Program Do?)** What does the following program print?

```
```cpp
// Exercise 4.21: Mystery2.cpp
#include <iostream>
using namespace std;

int main() {
    unsigned int count{1};

    while (count <= 10) {
        cout << (count % 2 == 1 ? "****" : "+-----+")
            << endl;
        ++count;
```
```