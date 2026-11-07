```
```cpp
// constructor
SalariedCommissionEmployee::SalariedCommissionEmployee(
    std::string_view name, double salary, double grossSales,
    double commissionRate)
    : SalariedEmployee{name, salary} { // call base-class constructor

    setGrossSales(grossSales); // validate & store gross sales
    setCommissionRate(commissionRate); // validate & store commission rate
}

// set gross sales amount
void SalariedCommissionEmployee::setGrossSales(double grossSales) {
    if (grossSales < 0.0) {
        throw std::invalid_argument("Gross sales must be >= 0.0");
    }

    m_grossSales = grossSales;
}

// return gross sales amount
double SalariedCommissionEmployee::getGrossSales() const {
    return m_grossSales;
}

// return commission rate
void SalariedCommissionEmployee::setCommissionRate(
    double commissionRate) {

    if (commissionRate <= 0.0 || commissionRate >= 1.0) {
        throw std::invalid_argument(
            "Commission rate must be > 0.0 and < 1.0");
    }

    m_commissionRate = commissionRate;
}

// get commission rate
double SalariedCommissionEmployee::getCommissionRate() const {
    return m_commissionRate;
}

// calculate earnings--uses SalariedEmployee::earnings()
double SalariedCommissionEmployee::earnings() const {
    return SalariedEmployee::earnings() +
        getGrossSales() * getCommissionRate();
}

// returns string representation of SalariedCommissionEmployee object
std::string SalariedCommissionEmployee::toString() const {
    return std::format(
        "Gross sales: ${:.2f}\ncommission rate: {:.2f}%\n",
        SalariedEmployee::toString(), getGrossSales(), getCommissionRate());
}
```
```

Fig. 10.5 | Class SalariedCommissionEmployee member-function definitions. (Part 2 of 2.)