```
// set base salary
void BasePlusCommissionEmployee::setBaseSalary(double salary) {
   if (salary < 0.0) {
      throw invalid_argument("Salary must be >= 0.0");
   }

   baseSalary = salary;
}

// return base salary
double BasePlusCommissionEmployee::getBaseSalary() const {
   return baseSalary;
}

// calculate earnings
double BasePlusCommissionEmployee::earnings() const {
   return baseSalary + (commissionRate * grossSales);
}

// return string representation of BasePlusCommissionEmployee object
string BasePlusCommissionEmployee::toString() const {
   ostringstream output;
   output << fixed << setprecision(2); // two digits of precision
   output << "base-salaried commission employee: " << firstName <<
      << lastName << "\nsocial security number: " << socialSecurityNumber
      << "\ngross sales: " << grossSales
      << "\ncommission rate: " << commissionRate
      << "\nbase salary: " << baseSalary;
   return output.str();
}
```

Fig. 11.8 **BasePlusCommissionEmployee** class represents an employee who receives a base salary in addition to a commission.

# Defining Class

# `BasePlusCommissionEmployee`

The `BasePlusCommissionEmployee` header (**Fig. 11.7**) specifies class `BasePlusCommissionEmployee`'s **public** services, which include the `BasePlusCommissionEmployee` constructor (lines 11–12) and member functions `earnings` (line 32) and `toString` (line 33). Lines 14–30