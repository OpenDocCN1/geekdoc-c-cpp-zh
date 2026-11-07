# 3.2.5  Using the Special Copy/Move Member Functions

Let us test the class Customer with a small program:

basics/customerimpl.cpp

```
#include "customerimpl.hpp"
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

int main()
{
    std::vector<Customer> coll;
    for (int i=0; i<12; ++i) {
        coll.push_back(Customer("TestCustomer " + std::to_string(i-5)));
    }

    std::cout << "----- sort()\n";
    std::sort(coll.begin(), coll.end(),
              [] (const Customer& c1, const Customer& c2) {
                  return c1.getName() < c2.getName();
              });
}
```

# Initialization

The first part is the initialization of the vector with 12 customers:

```
std::vector<Customer> coll;
for (int i=0; i<12; ++i) {
    coll.push_back(Customer("TestCustomer " + std::to_string(i-5)));
}
```

This initialization might have the following output:

```
MOVE TestCustomer -5
MOVE TestCustomer -4
COPY TestCustomer -5
MOVE TestCustomer -3
COPY TestCustomer -5
COPY TestCustomer -4
MOVE TestCustomer -2
MOVE TestCustomer -1
COPY TestCustomer -5
COPY TestCustomer -4
COPY TestCustomer -3
COPY TestCustomer -2
```