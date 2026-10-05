# 17.6. FINE TUNING INHERITANCE

```
LogComparer(bool (*f) (int, int), const std::string& filename);

// The destructor must close the log file
~LogComparer();

#endif
```

The LogComparer class overrides the compare_impl and swap_impl methods. Instances of the LogComparer class use an ofstream object to record logging information to a text file.

The implementation of the LogComparer methods can be found in Listing 17.22 (logcomparer.cpp).

# Listing 17.22: logcomparer.cpp

```
#include "logcomparer.h"
#include <cstdlib>
#include <iostream>

using namespace std;

// Method that actually performs the comparison
// Derived classes may override this method
bool LogComparer::compare_impl(int m, int n) {
    f << "Comparing " << m << " to " << n << endl;
    // Base class method does the comparison
    return LogComparer::compare_impl(m, n);
}

// Method that actually performs the swap
// Derived classes may override this method
void LogComparer::swap_impl(int& m, int& n) {
    f << "Swapping " << m << " and " << n << endl;
    int temp = m;
    m = n;
    n = temp;
}

// The client must initialize a LogComparer object with a
// suitable function and the file name of the
// text file to receive logging messages.
LogComparer::LogComparer(bool (*f) (int, int), const std::string filename)
    : f(f) {
    f.open(filename);
    if (!f.good()) {
        f.close();
        cout << "Could not open log file " << filename
             << " for writing" << endl;
        exit(1);
    }
}

// Destructor closes the log file
LogComparer::~LogComparer() {
    f.close();
}
```

©2014 Richard L. Halterman Draft date: January 26, 2014