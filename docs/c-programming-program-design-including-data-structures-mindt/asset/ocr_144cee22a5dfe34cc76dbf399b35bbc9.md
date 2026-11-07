```
```cpp
class employee
{
public:
    void setData(string n = "", string d = "", int a = 0,
                 double p = 0);

    void setName(string n);
    string getName() const;
    void setDepartment(string dept);
    string getDepartment() const;
    void setAge(int a);
    int getAge() const;
    void setPay(double p);
    double getPay() const;

    employee(string n = "", string d = "", int a = 0,
             double p = 0);

private:
    string name;
    string department;
    int age;
    double pay;
};
```
```

Identify and correct errors in the following class definition? (2)

```
```cpp
class hourlyEmployee: public class employee
{
public::
    void setData(string n = "", string d = "", int a = 0,
                 double p = 0, double hrsWk = 0,
                 double payRate = 0.0);
    // Data members are set according to the parameters.
    // Values assigned to numeric data is nonnegative.

    void setHoursWorked(double hrsWk) const;
    // Function to set hours worked.
    // if hrsWk >= 0, hoursWorked = hrsWk;
    // Otherwise hoursWorked = 0;

    double getHoursWorked() const;
    // returns the value of hoursWorked.

    void setHourlyPayRate(double payRate);
    // Function to set hourly pay rate.
    // if payRate >= 0, hourlyPayRate = payRate;
    // Otherwise hourlyPayRate = 0;

    double getHourlyPayRate() const;
    // returns the value of hourlyPayRate.

    void setPay() const;
    // Function to set pay.
    // if hoursWorked >= 0 and hourlyPayRate >= 0
    //    pay = hoursWorked * hourlyPayRate;
    // Otherwise pay = 0.0;
```
```