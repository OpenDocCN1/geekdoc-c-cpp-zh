
# SOURCE 4.3: THE IMPORT CLASS AND EXAMPLE IMPLEMENTATION

```cpp
// Import.h
#pragma once

#include "Utils.h"

#include <string>
using std::string;

class Import {
public:
    Import() {}
    virtual ~Import() {}

    // Member function declarations
    vector<vector<double>> GetData(const string& fileName); // GetData()
private:
    // Member variable declarations
    Utils m_utils; // An instance of the Utils class
};

// Import.cpp
#include "Import.h"

#include <fstream>
#include <sstream>
#include <iostream>
using std::cout;
using std::ifstream;
using std::stringstream;

// Member functions definitions
vector<vector<double>> Import::GetData(const string& fileName)
{
    int ROW = 0, COLS = 0; // Initialise rows and columns
    string line, tmp;
    stringstream ss; // Create a stringstream object

    ifstream file(fileName); // Add file to fstream

    getline(file, line); // Remove file header
    ss.clear(); // Clear stringstream

    ss << line;
    while (ss >> tmp) {
        COLS++; // Determine # columns (COLS) in file
    }
    vector<vector<double>> data; // Declare a 2D vector of doubles
    vector<double> v(COLS); // Declare a 1D vector of doubles

    if(file.is_open()) {
        while (file.good()) {
            {
                data.push_back(v); // Add a new row to data
                for (int COL=0; COL<COLS; COL++) {
                    file >> data[ROW][COL]; // Fill the row with elements
                }
            }
            ROW++; // Keep track of the current ROW and increment
        }
        data.pop_back(); // Remove null values at end of data
        std::cout << "\nFile: " << fileName << " \n";
        std::cout << " Imported " << data.size() * (COLS - 1) << " \n" values successfully!\n";
        file.close(); // Close file
    } else {
        m_utils.ErrorChk("Unable to load file");
    }

    return data;
}

// main.cpp
#include "Import.h"
#include <windows.h>
#include <iostream>
using std::cout;
using std::cin;

int main()
{
  SetConsoleTitle(L"Console Output");

  vector<vector<double>> data; // Declare a 2D vector for the data values
  Import ctai; // Create an instance of the Import class

  // Call GetData() member function from the Import class
  data = ctai.GetData("./data/cta_index.dat");

  vector<string> v; // Declare a 1D vector for the hedge fund name
  v.push_back("CTA");

  cout << "\nPrinting first 18:\n";
  Utils::PrintFile(data, v, 18); // Print first 18

  cin.get();
  return 0;
}
```

![](img/2d1ac831a270b8b08f8b8ec2205913dc_137_0.png)

Note that there are numerous other ways of manipulating files in C++ but this gives us a standard method that we can easily use and is more than adequate for our purposes. In import.h we have instantiated the Utils class in the header variable m_utils. This allows us access to the ErrorChk() method from the Utils class using dot notation i.e. m_utils.ErrorChk(). However, we must include the Utils class header file (Utils.h) within the Import class header to allow this access.

![](img/2d1ac831a270b8b08f8b8ec2205913dc_138_0.png)

FIGURE 4.2 Bar chart of the monthly returns for the CTA Index

# 4.4 BASIC PERFORMANCE PLOTS

## 4.4.1 Value Added Index

Extracting any valuable information from a time series of hedge fund returns is practically impossible with a large set of data in tabular format. Consider the hypothetical monthly returns for a CTA Index; a total of 72 individual positive and negative returns. A simple bar chart of the data, as shown in Figure 4.2, gives an instant visualisation of the performance of the CTA Index over the period as well as identifying areas of highs and lows.

The Value Added Index (VAI) is a statistic that shows the performance of a $1000 investment on a set of returns for a hedge fund with specific reporting frequency e.g. daily, monthly. The VAI can be calculated for daily, weekly or monthly depending on the reporting frequency. The VAI is given by:
$VAI_{t+1} = VAI_t(1 + r_t)$

The monthly VAI (VAI) for the CTA Index of monthly returns is shown in Figure 4.3. Reading off the final value of $1000 investment in the CTA Index gives a VAI; however, it does not tell us much about hedge funds also report daily and weekly returns, but monthly is the most common. A hedge fund may just provide a series of Net Asset Values (NAV) in which case they can be converted into an equivalent series of periodic returns $r_{t_1,t_2} = \frac{NAV_{t_2}}{NAV_{t_1}} - 1$ where is the return for the hedge fund between time $t_1$ and $t_2$ ($t_2 > t_1$).

![](img/2d1ac831a270b8b08f8b8ec2205913dc_139_0.png)

FIGURE 4.3 The VAI plot for the Index since inception. Source 4.4 shows the VAI() member function and method implementation for the Stats class.

# SOURCE 4.4: THE VAI MEMBER FUNCTION AND METHOD IMPLEMENTATION

```cpp
// Stats.h
#pragma once

#include "Utils.h"

class Stats {
public:
    Stats() {}
    virtual ~Stats() {}

    // Member function declarations
    double VAI(const vector<vector<double>>& v); // VAI()
private:
    // Member variable declarations
    Utils m_utils; // An instance of the Utils class
};

// Member functions definitions
// VAI()
double Stats::VAI(const vector<vector<double>>& v)
{
    unsigned int n = v.size(); // Declare an unsigned integer
    double vai; // Define a double for VAI

    vai = 1000.0; // Initialise to 1000

    // Calculate VAI using Eq. (3.1)
    for(unsigned int i=0; i<n; i++)
    { 
        vai *= (1 + v[i][v[0].size()-1);
    }
    return vai;
}

// main.cpp
#include "Import.h"
#include "Stats.h"
#include <windows.h>
#include <iostream>
using std::cout;
using std::cin;

int main()
{
    SetConsoleTitle(L"Console Output");

    vector<vector<double>> data; // Declare a 2D vector for the data values
    Import ctai; // Create an instance of the Import class

    // Call GetData() member function from the Import class
    data = ctai.GetData("./data/cta_index.dat");

    Stats stats; // Create an instance of the Stats class
    double vai; // Declare a double for the VAI value

    // Call VAI() method function from the Stats class
    vai = stats.VAI(data);

    // Output result
    cout << "\nVAI($)" << vai << "\n";

    cin.get();
    return 0;
}
```

![](img/2d1ac831a270b8b08f8b8ec2205913dc_141_0.png)

Using [v[0].size()-1] in the for loop allows us access to the columns in the V2DD container and we have subtracted one since the first column is just period data i.e. 1, 2, 3, etc.

## 4.4.2 Histograms

A histogram is a graphical summary of the frequency distribution of a set of empirical data, for example as a time series of monthly hedge returns (or NAVs). The frequency is an absolute value in which each value represents the actual count of the number of occurrences of a particular value in a group of data. Relative frequencies involve normalising the frequencies through division of the absolute frequency by the total number of observations in the group of data. Knowing the max and min values of the monthly returns it is possible to set a range that encompasses all the monthly returns in the data set. This range is divided into equal intervals (bins) and an absolute frequency determined for each number of values that fall within each bin. Once the absolute values have been determined, a relative frequency can be calculated by dividing each absolute frequency by the sum of absolute frequencies i.e. 72. An example of a histogram for the CTA Index is shown in Figure 4.4.

The histogram is a very useful representation of a set of hedge fund returns over a specific time period, gives a good visual representation of the shape of the distribution and highlights areas of high negative and positive returns.

![](img/2d1ac831a270b8b08f8b8ec2205913dc_142_0.png)

FIGURE 4.4 A histogram for the CTA Index of monthly returns

# 4.5 PROABILITY DISTRIBUTIONS

In order to understand probability distributions, it is important to know what is meant by a random variable. When a numerical value of a variable is determined by an unknown (or chance) event, that variable is said to be random. Random variables can either be discrete or continuous. For example, suppose an experiment consists of flipping a coin six times and recording the number of heads that appear after each toss. The number of heads from a random process (i.e. flipping the coin) and the actual number is a value between 0 and 6 i.e. a finite integer. Therefore, the number of heads is said to be a discrete random variable.
