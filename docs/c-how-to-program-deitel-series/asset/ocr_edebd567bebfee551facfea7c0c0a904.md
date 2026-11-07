```
```cpp
// return commission rate
double BasePlusCommissionEmployee::getCommissionRate() const
{
    return commissionRate;
} // end function getCommissionRate

// set base salary
void BasePlusCommissionEmployee::setBaseSalary( double salary )
{
    if ( salary >= 0.0 )
        baseSalary = salary;
    else
        throw invalid_argument( "Salary must be >= 0.0" );
} // end function setBaseSalary

// return base salary
double BasePlusCommissionEmployee::getBaseSalary() const
{
    return baseSalary;
} // end function getBaseSalary

// calculate earnings
double BasePlusCommissionEmployee::earnings() const
{
    return baseSalary + ( commissionRate * grossSales );
} // end function earnings

// print BasePlusCommissionEmployee object
void BasePlusCommissionEmployee::print() const
{
    cout << "base-salaried commission employee: " << firstName << ' '
         << lastName << "\nsocial security number: " << socialSecurityNumber
         << "\ngross sales: " << grossSales
         << "\ncommission rate: " << commissionRate
         << "\nbase salary: " << baseSalary;
} // end function print
```
```

**Fig. 11.8** | BasePlusCommissionEmployee class represents an employee who receives a base salary in addition to a commission. (Part 3 of 3.)

# Defining Class BasePlusCommissionEmployee

The BasePlusCommissionEmployee header (Fig. 11.7) specifies class BasePlusCommissionEmployee’s public services, which include the BasePlusCommissionEmployee constructor (lines 12–13) and member functions earnings (line 33) and print (line 34). Lines 15–31 declare public get and set functions for the class’s private data members (declared in lines 36–41) firstName, lastName, socialSecurityNumber, grossSales, commissionRate and baseSalary. These variables and member functions encapsulate all the necessary features of a base-salaried commission employee. Note the similarity between this class and class CommissionEmployee (Figs. 11.4–11.5)—in this example, we do not yet exploit that similarity.

Class BasePlusCommissionEmployee’s earnings member function (defined in lines 104–107 of Fig. 11.8) computes the earnings of a base-salaried commission employee.