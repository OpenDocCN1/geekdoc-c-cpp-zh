![](bbox=[0.175, 0.095, 0.775, 0.335])

FIGURE 4.3 The VAMI plot for the Index since inception. Source 4.4 shows the VAI() member function and method implementation for the Stats class.

the performance of the Index since inception. Source 4.4 shows the VAI() member function and method implementation for the Stats class.

# SOURCE 4.4: THE VAI()) MEMBER FUNCTION AND METHOD IMPLEMENTATION

```
// Stats.h
#pragma once;

#include "Utils.h"

class Stats {
public:
    Stats() {}
    virtual -Stats() {}

    // Member function declarations
DBL VAI(const V2DD& v); // VAI()
private:
    // Member variable declarations
    Utils m_utils; // An instance of the Utils class
};

// Member functions definitions
// VAI()
DBL Stats::VAI(const V2DD& v)
{
```