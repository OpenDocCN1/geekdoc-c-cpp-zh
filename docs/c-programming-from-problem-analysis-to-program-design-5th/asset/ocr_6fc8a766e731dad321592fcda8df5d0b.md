![](bbox=[0.182, 0.107, 0.912, 0.333])

**FIGURE 13-5** UML class diagram of the class `partTimeEmployee` and inheritance hierarchy

The definitions of the member functions of the class `partTimeEmployee` are as follows:

```
```cpp
void partTimeEmployee::print() const
{
    personType::print(); //print the name of the employee
    cout << "'s wages are: $" << calculatePay() << endl;
}

double partTimeEmployee::calculatePay() const
{
    return (payRate * hoursWorked);
}

void partTimeEmployee::setNameRateHours(string first,
                                         string last, double rate, double hours)
{
    personType::setName(first, last);
    payRate = rate;
    hoursWorked = hours;
}

//Constructor
partTimeEmployee::partTimeEmployee(string first, string last,
                                    double rate, double hours)
    : personType(first, last)
{
    if (rate >= 0)
        payRate = rate;
    else
        payRate = 0;

    if (hours >= 0)
        hoursWorked = hours;
    else
        hoursWorked = 0;
}
```
```