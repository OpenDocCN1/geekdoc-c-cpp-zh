
reads one value at a time from the keyboard and stores the value in element `a[0]`.

```cpp
// Fig. 7.6: Fig07_06.cpp
// Compute the sum of the elements of an array.
#include <iostream>
#include <array>
using namespace std;

int main() {
   const size_t arraySize{4}; // specifies size of array
   array<int, arraySize> a{10, 20, 30, 40};
   int total{0};

   // sum contents of array a
   for (size_t i{0}; i < a.size(); ++i) {
      total += a[i];
   }

   cout << "Total of array elements: " << total << endl;
}
```

```text
Total of array elements: 100
```

**Fig. 7.6** Compute the sum of the elements of an `array`.

### 7.4.5 Using a Bar Chart to Display `array` Data Graphically

Many programs present data to users graphically. For example, numeric values are often displayed as bars in a bar chart, with longer bars representing proportionally larger numeric values. One simple way to display numeric data graphically is with a bar chart that shows each numeric value as a bar of asterisks (`*`).

Professors often like to examine grade distributions on an exam. A professor might graph the number of grades in each of several categories to visualize the grade distribution. Suppose the grades were 87, 68, 94, 100, 83, 78, 85, 91, 76 and 87. There was one grade of 100, two grades in the 90s, four grades in the 80s, two grades in the 70s, one grade in the 60s and no grades below 60. Our next program (Fig. 7.7) stores this data in an `array` of 11 elements, each corresponding to a grade range. For example, `n[0]` indicates the number of grades in the range 0–9, `n[7]` indicates the number of grades in the range 70–79 and `n[10]` indicates the number of grades of 100. The `GradeBook` classes that you’ll see in Figs. 7.13 and 7.19 contain code that calculates grade frequencies based on a set of grades. In this example, we initialize the array `n` with frequency values.

The program ([Fig. 7.7](#)) reads the numbers from the `array` and graphs the information as a bar chart, displaying each grade range followed by a bar of asterisks indicating the number of grades in that range. To label each bar, lines 17–25 output a grade range (e.g., `"70–79: "`) based on the current value of counter variable `i`. The *nested* `for` statement (lines 28–30) outputs the current bar as the appropriate number of asterisks. Note the loop-continuation condition in line 28 (`stars < n[i]`). Each time the program reaches the *inner* `for`, the loop counts from `0` up to `n[i]`, thus using a value in `array n` to determine the number of asterisks to display. In this example, `n[0]–n[5]` contain zeros because no students received a grade below 60. Thus, the program displays no asterisks next to the first six grade ranges.

```cpp
// Fig. 7.7: Fig07_07.cpp
// Bar chart printing program.
#include <iostream>
#include <iomanip>
#include <array>
using namespace std;

int main() {
   const size_t arraySize{11};
   array<unsigned int, arraySize> n{0, 0, 0, 0, 0, 0, 1, 2, 4, 2, 1};

   cout << "Grade distribution:" << endl;

   // for each element of array n, output a bar of the chart
   for (size_t i{0}; i < n.size(); ++i) {
      // output bar labels ("0-9:", ..., "90-99:", "100:")
      if (i == 0) {
         cout << " 0-9: ";
      }
      else if (i == 10) {
         cout << " 100: ";
      }
      else {
         cout << i * 10 << "-" << (i * 10) + 9 << ": ";
      }

      // print bar of asterisks
      for (unsigned int stars{0}; stars < n[i]; ++stars) {
         cout << '*';
      }

      cout << endl; // start a new line of output
   }
}
```

```text
Grade distribution:
 0-9:
10-19:
20-29:
30-39:
40-49:
50-59:
60-69: *
70-79: **
80-89: ****
90-99: **
 100: *
```

**Fig. 7.7** Bar chart printing program.

### 7.4.6 Using the Elements of an `array` as Counters

Sometimes, programs use counter variables to summarize data, such as the results of a survey. In **Fig. 6.7**, we used separate counters in our die-rolling program to track the number of occurrences of each side of a die as the program rolled the die 60,000,000 times. An `array` version of this program is shown in **Fig. 7.8**. This version also uses the new C++11 random-number generation capabilities that were introduced in **Section 6.9**.

**Figure 7.8** uses the `array` `frequency` (line 17) to count the occurrences of die value. *The single statement* in line 21 of this program replaces the entire `switch` statement in lines 22–43 of **Fig. 6.7**. Line 21 uses a random value to determine which `frequency` element to increment during each iteration of the loop.

```cpp
// Fig. 7.8: Fig07_08.cpp
// Die-rolling program using an array instead of switch.
#include <iostream>
#include <iomanip>
#include <array>
#include <random>
#include <ctime>
using namespace std;

int main() {
    // use the default random-number generation engine to
    // produce uniformly distributed pseudorandom int values from 1 to 6
    default_random_engine engine(static_cast<unsigned int>(time(0)));
    uniform_int_distribution<unsigned int> randomInt(1, 6);

    const size_t arraySize{7}; // ignore element zero
    array<unsigned int, arraySize> frequency{}; // initialize to 0s

    // roll die 60,000,000 times; use die value as frequency index
    for (unsigned int roll{1}; roll <= 60'000'000; ++roll) {
        ++frequency[randomInt(engine)];
    }

    cout << "Face" << setw(13) << "Frequency" << endl;

    // output each array element's value
    for (size_t face{1}; face < frequency.size(); ++face) {
        cout << setw(4) << face << setw(13) << frequency[face] << endl;
    }
}
```

```text
Face    Frequency
  1       9997901
  2       9999110
  3      10001172
  4      10003619
  5       9997606
  6      10000592
```

**Fig. 7.8** Die-rolling program using an `array` instead of `switch`.

The calculation in line 21 produces a random subscript from 1 to 6, so `array frequency` must be large enough to store six counters. We use a seven-element `array` in which we ignore `frequency[0]`—it’s clearer to have the die face value 1 increment `frequency[1]` than `frequency[0]`. Thus, each face value is used *directly* as a subscript for `array frequency`. We also replace lines 46–51 of **Fig. 6.7** by looping through `array frequency` to output the results (**Fig. 7.8**, lines 27–29).

### 7.4.7 Using `arrays` to Summarize Survey Results

Our next example uses `arrays` to summarize the results of data collected in a survey. Consider the following problem statement:

- *Twenty students were asked to rate on a scale of 1 to 5 the quality of the food in the student cafeteria, with 1 being “awful” and 5 being “excellent.” Place the 20 responses in an integer `array` and determine the frequency of each rating.*

This is a popular type of `array`-processing application ([Fig. 7.9](#)). We wish to summarize the number of responses of each rating (that is, 1–5). The `array` `responses` (lines 14–15) is a 20-element integer `array` of the students’ responses to the survey. The `array` `responses` is declared `const`, as its values do not (and should not) change. We use a six-element `array` `frequency` (line 18) to count the number of occurrences of each response. Each element of the `array` is used as a counter for one of the survey responses and is initialized to zero. As in [Fig. 7.8](#), we ignore `frequency[0]`.

```cpp
// Fig. 7.9: Fig07_09.cpp
// Poll analysis program.
#include <iostream>
#include <iomanip>
#include <array>
using namespace std;

int main() {
   // define array sizes
   const size_t responseSize{20}; // size of array responses
   const size_t frequencySize{6}; // size of array frequency

   // place survey responses in array responses
   const array<unsigned int, responseSize> responses{
      1, 2, 5, 4, 3, 5, 2, 1, 3, 1, 4, 3, 3, 3, 3, 2, 3, 2, 2, 5};

   // initialize frequency counters to 0
   array<unsigned int, frequencySize> frequency{};

   // for each answer, select responses element and use that value
   // as frequency subscript to determine element to increment
   for (size_t answer{0}; answer < responses.size(); ++answer) {
      ++frequency[responses[answer]];
   }

   cout << "Rating" << setw(12) << "Frequency" << endl;

   // output each array element's value
   for (size_t rating{1}; rating < frequency.size(); ++rating) {
      cout << setw(6) << rating << setw(12) << frequency[rating] << endl;
   }
}
```

| Rating | Frequency |
|---:|---:|
| 1 | 3 |
| 2 | 5 |
| 3 | 7 |
| 4 | 2 |
| 5 | 3 |

**Fig. 7.9** Poll analysis program.

The first `for` statement (lines 22–24) takes the responses one at a time from the `array responses` and increments one of the five counters in the `frequency` array (`frequency[1]` to `frequency[5]`). The key
