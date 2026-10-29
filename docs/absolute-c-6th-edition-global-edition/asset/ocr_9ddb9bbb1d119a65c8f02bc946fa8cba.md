# Display 15.6 Interface for the Abstract Class Employee (part 2 of 2)

```
18    void setSsn(const string& newSsn);
19    void setNetPay(double newNetPay);
20    virtual void printCheck() const = 0;
21    private:
22    string name;
23    string ssn;
24    double netPay;
25    };
26    }//SavitchEmployees
27    #endif //EMPLOYEE_H
```

A pure virtual function

# Self-Test Exercises

3. Is it legal to have an abstract class in which all member functions are pure virtual functions?

4. Given the definition of the class Employee in Display 15.6, which of the following are legal?

+   a. Employee joe;
+      joe = Employee();

```
b. class HourlyEmployee : public Employee
{
public:
    HourlyEmployee();
    <Some more legal member function definitions, none of which are pure virtual functions>
private:
    double wageRate;
    double hours;
};
int main()
{
    Employee joe;
    joe = HourlyEmployee();
```

```
c. bool isBossOf(const Employee& e1, const Employee& e2);
```