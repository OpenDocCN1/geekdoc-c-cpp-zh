# Compensation Model Commission

Class Commission (Figs. 20.9–20.10) defines the compensation model for an Employee who gets paid commission based on gross sales. Like Salaried, this Commission is not a derived class. So, its earnings and toString member functions do not override base-class virtual functions, as they did in Section 10.11.

```
```cpp
// Fig. 20.9: Commission.h
// Commission compensation model.
#pragma once
#include <string>

class Commission {
public:
   Commission(double grossSales, double commissionRate);
   double earnings() const;
   std::string toString() const;
private:
   double m_grossSales{0.0};
   double m_commissionRate{0.0};
};
```
```

**Fig. 20.9** | Commission compensation model.

```
```cpp
// Fig. 20.10: Commission.cpp
// Commission member-function definitions.
#include <format>
#include <stdexcept>
#include "Commission.h" // class definition

// constructor
Commission::Commission(double grossSales, double commissionRate)
   : m_grossSales{grossSales}, m_commissionRate{commissionRate} {

   if (m_grossSales < 0.0) {
      throw std::invalid_argument("Gross sales must be >= 0.0");
   }

   if (m_commissionRate <= 0.0 || m_commissionRate >= 1.0) {
      throw std::invalid_argument(
         "Commission rate must be > 0.0 and < 1.0");
   }
}

// calculate earnings
double Commission::earnings() const {
   return m_grossSales * m_commissionRate;
}
```
```

**Fig. 20.10** | Commission member-function definitions. (Part 1 of 2.)