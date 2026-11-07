is usually fixed for a year. In addition, a full-time employee may receive a bonus. On the other hand, the salary of a part-time employee is usually calculated according to the pay rate per hour and the number of hours worked. In this example, we first define the class employeeType, derived from the class personType, to store an employee’s name and ID. We include functions to set the ID and retrieve the ID. We also include pure virtual functions print and calculatePay to print an employee’s data, which includes the employee’s ID, name, and wages.

From the class employeeType, we derive the classes fullTimeEmployee and partTimeEmployee and provide the definitions of the pure virtual functions of the class employeeType.

The definition of the class employeeType is:

```
```cpp
class employeeType: public personType
{
public:
    virtual void print() const = 0;
       //Function to output employee's data.

    virtual double calculatePay() const = 0;
       //Function to calculate and return the wages.
       //Postcondition: Pay is calculated and returned

    void setId(long id);
       //Function to set the ID.
       //Postcondition: personId = id

    long getId() const;
       //Function to retrieve the id.
       //Postcondition: returns personId

    employeeType(string first = "", string last = "",
                 long id = 0);
       //Constructor with parameters
       //Sets the first name, last name, payRate, and
       //hoursWorked according to the parameters. If
       //no value is specified, the default values are
       //assumed.
       //Postcondition: firstName = first;
       //               lastName = last; personId = id

private:
    long personId;       //stores the id
};
```
```

The definitions of the constructor and functions of the class employeeType that are not pure virtual are:

```
```cpp
void employeeType::setId(long id)
{
    personId = id;
}
```
```