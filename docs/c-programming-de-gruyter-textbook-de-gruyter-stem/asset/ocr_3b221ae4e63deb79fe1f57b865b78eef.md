# 150 4 Class and Object

| employee |
| # individualEmpNo : int |
| # grade : int |
| # accumPay : float |
| + employee() |
| ~employee() |
| +IncreaseEmpNo(int) : void |
| + promote(int) : void |
| + SetaccumPay(float) : void |
| + GetIndividualEmpNo() : int |
| + Getgrade() : int |
| + GetaccumPay() : float |

![](bbox=[0.433, 0.267, 0.725, 0.279])

# 4.6.2 Source Code and Description

**Example 4.7**: Personnel information management.
The whole program is divided into two independent documents: employee.h includes declaration and definition of classes, and 4_5.cpp is the main function.

```
//employee.h
class employee
{
protected:
    int individualEmpNo; //id
    int grade; //grade
    float accumPay; //payment
public:
    employee(); //constructor
    ~employee(); //destructor
    void IncreaseEmpNo(int); //increasing id function
    void promote(int); //promoting function
    void SetaccumPay(float); //setting payment function
    int GetIndividualEmpNo(); //getting id function
    int Getgrade(); //getting grade function
    float GetaccumPay(); //getting payment function
};

employee::employee()
{
    individualEmpNo=1000; //max id of employee is now 1000
    grade=1; //initial grade is 1
    accumPay=0.0; //initial payment is 0
}

employee::~employee() {} //destructor is empty
```