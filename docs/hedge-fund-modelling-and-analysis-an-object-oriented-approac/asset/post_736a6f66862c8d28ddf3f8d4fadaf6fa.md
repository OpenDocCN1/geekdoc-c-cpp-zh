
Tracking error may be calculated from historical performance data or estimated for future returns. The former is called *ex-post*, and the latter *ex-ante* tracking error. Mathematically, tracking error (*TE*) can be defined in terms of the standard deviation (*SD*), such that:

```
$TE = \sqrt{\frac{1}{N-1} \sum_{i=1}^{N} (r_{N-1,N} - \rho^{bm}_{1,N})^2}} \quad (3.1)$
```

where $N$ is the total number of sample data points, $r_{N-1,N}$ is the hedge fund return and $\rho^{bm}_{1,N}$ is the benchmark return. Many practitioners have argued the quadratic form of the *TE* is difficult to interpret, and that fund managers generally think in terms of linear and not quadratic deviations from a benchmark. In this case, TE in terms of the mean absolute deviations (*MAD*) can be written as:

```
$MAD = \frac{1}{N-1} \sum_{i=1}^{N} |r_{N-1,N} - \rho^{bm}_{1,N}| \quad (3.2)$
```

In this chapter we have discussed the hedge fund databases available in the market and the range of services and products they offer. We have highlighted the fact that the hedge fund industry is highly heterogeneous, which makes the construction of a useful market index that comprises the available hedge fund universe very difficult. Moreover, the issues relating to the different ways in which hedge funds report to commercial databases create a variety of data biases which can lead to vendors publishing misleading and incomplete performance measures. Non-investable hedge fund indices taken from a particular database; however, such vendors have diverse selection criteria and methods of index construction leading to many different published indices. More-investable indices. More recently, many index providers have developed investable indices that offer a low-cost investment and exposure to the hedge fund industry. Nevertheless, one should be fully aware of the limitations and constraints before accepting a particular index as a valued industry benchmark.

In the following chapters we will build and develop a quantitative and theoretical approach to modelling and analysing hedge funds. Chapter 4 begins this process by introducing the main statistical methods and techniques applied to hedge funds.

## CHAPTER 4

## Statistical Analysis

In order for hedge fund managers to make informed decisions with regard to their investments it is essential that several key statistical analyses are performed. This will usually involve analysing a time series of periodic hedge fund returns to ascertain relevant statistical properties of hedge in order to make critical inference about the characteristics and performance of the hedge fund. Many visual and mathematical methods are available allow hedge fund managers to understand the underlying data structure and identify potential anomalies that may need further investigation whilst allowing managers to make informed decisions. It is also important that a serious investor or hedge fund manager have a working knowledge of many of the probability and statistical concepts encountered in the industry so as to be confident and knowledgeable when explaining and discussing their hedge fund investment strategies to potential investors.

Chapter 4 covers the main concepts, principles and techniques employed in the statistical analysis of hedge fund returns. Both visual and theoretical methods are presented which show how to extract and interpret the informational content and underlying characteristics within a periodic time series of hedge fund returns. However, delving into those issues we will briefly discuss the basis of the class structure we are going to build upon as we go through each chapter.

To implement the statistical methods described in this chapter we will be developing a Stats class. Source 4.1 shows the basic skeleton of the Stats class which we will add to as and when necessary.

### SOURCE 4.1: THE SKELETON OF THE STATS CLASS

```cpp
// Stats.h
#pragma once

class Stats {
public:
    Stats() {}
    virtual ~Stats() {}
private:
    };

// Stats.cpp
#include "Stats.h"
```

Notice that the default constructor and destructor have been declared and defined in the header file by removing the semi-colon (;) and adding the opening and closing braces ({}). We can do this since we are not explicitly using either the constructor or destructor to initialise any variables or perform any tasks in the class.

The Utils class contains several helper functions to assist with the other classes and provide methods that we will make use on many occasions to simplify general tasks, for example printing to the console output and error checking. The Utils class and associated methods are shown in Source 4.2.

### SOURCE 4.2: THE UTILS CLASS

```cpp
// Utils.h
#pragma once

#include <iostream>
#include <string>
#include <vector>
using std::string;
using std::vector;
```

```cpp
// typedef definitions
typedef unsigned int UINT;
typedef double DBL;
typedef vector<int> VID1;
typedef vector<float> V1DF;
typedef vector<double> V1DD;
typedef vector<vector<int>> V2DI;
typedef vector<vector<float>> V2DF;
typedef vector<vector<double>> V2DD;
```

```cpp
class Utils {
public:
    Utils() {}
    virtual ~Utils() {}

    // Member function declarations
    static void PrintResult(const V1DD& v, const int& WIDTH);
    void PrintResult();
    static void PrintFile(const V2DD& v, const V1DS& s, const int& n);
    void PrintFile();
    void ErrorChk(const string& s); // ErrorChk()
private:
    // Member variable definitions
};
```

```cpp
// Utils.cpp
#include "Utils.h"

#include <iostream>
#include <iomanip>
using std::cout;
using std::cerr;

// Member function definitions
// PrintResult
void Utils::PrintResult(const V1DD& v, const int& WIDTH) {
    cout << fixed;
    for (int i = 0; i < v.size(); i++) {
        // Array flattening
        for (int j = 0; j < WIDTH; j++) {
            // logic for flattening
        }
    }
    cout << "\n";
}

// PrintFile
void Utils::PrintFile(const V2DD& v, const V1DS& s, const int& n) {
    cout << "\n";
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < v[i].size(); j++) {
            cout << left << setw(6) << v[i][j];
        }
        cout << "\n";
    }
}

// ErrorChk
void Utils::ErrorChk(const string& s) {
    cerr << "\n Run-time error...\n";
    cerr << " Message: " << s << "\n\n";
    cin.get();
    exit(1);
}
```
