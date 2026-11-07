# Missing Data

Bad data values and missing values can significantly impact data analysis. The Titanic dataset is missing the ages of 263 passengers. These are represented as ? in the CSV file. In this example, when we produce descriptive statistics for the passengers’ ages, we’ll filter out and ignore the missing values. Some data scientists advise against any attempts to insert “reasonable values.” Instead, they advocate clearly marking missing data and leaving it up to a data analytics package to handle the issue. Others offer strong cautions.

# Loading the Dataset

Figure 8.15 uses some C++20 ranges library features we introduced in Section 6.14. We broke the program into parts for discussion purposes. Lines 15–17 create and initialize a rapidcsv::Document object named titanic that loads "titanic.csv". The second and third arguments in line 16 are two of the default arguments used to initialize a Document object when you create it only by specifying the CSV filename. Recall from our discussion of default function arguments that when an argument is specified explicitly for a given parameter, all prior arguments in the argument list also must be specified explicitly. We provided the second and third arguments only so we could specify the fourth argument.

```
```cpp
// fig08_15.cpp
// Reading the Titanic dataset from a CSV file, then analyzing it.
#include <format>
#include <algorithm>
#include <cmath>
#include <iostream>
#include <numeric>
#include <ranges>
#include <rapidcsv.h>
#include <string>
#include <vector>

int main() {
    // load Titanic dataset; treat missing age values as NaN
    rapidcsv::Document titanic{"titanic.csv",
        rapidcsv::LabelParams{}, rapidcsv::SeparatorParams{},
        rapidcsv::ConverterParams{true}};
}
```
```

**Fig. 8.15** | Reading the Titanic dataset from a CSV file, then analyzing it.