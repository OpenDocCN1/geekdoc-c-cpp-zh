Figure 6.11 shows the output of the preceding code:

![](bbox=[0.21, 0.075, 0.77, 0.2])

# Figure 6.11: Creating a Delegate

Let’s now look at the most important parts of this program. The following code snippet shows how to define a delegate in the class that uses it:

```
public delegate Boolean IncrementAccountDelegate(Account a,double d);
public delegate Boolean DecrementAccountDelegate(Account a,double d);
```

The following code snippet shows how the delegates are passed and used into a class method:

```
if (d < 0)
    dec(accounts[nAcct], -d);
else
    inc(accounts[nAcct], d);
```

The code that creates new delegates of the appropriate types and connects them to real methods that do the processing is shown in the following code snippet:

```
AccountDB.IncrementAccountDelegate iad =
new AccountDB.IncrementAccountDelegate(ah.AccountInc);
AccountDB.DecrementAccountDelegate dad =
new AccountDB.DecrementAccountDelegate(ah.AccountDec);
```

Let’s now learn to declare and instantiate a delegate

# Declaring and Instantiating a Delegate

Let’s create a Console application, named SampleDelegate (also available on the CD), for declaring and instantiating a delegate. Listing 6.10 shows the code of the Program.cs file of the SampleDelegate application:

Listing 6.10: Showing the Code of the Program.cs File

```
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace SampleDelegate
{
public struct Employee
{
public string strname;
public string LName;
public decimal Sal;
public bool Stat;
public Employee(string name, string lname, decimal salary, bool status) {
strname = name;
LName = lname;
Sal = salary;
Stat = status;
}
}
// declaring a delegate type
public delegate void EmployeeDelegateOperT(Employee employee);
public class EmpDB
{
// List of all Employees in the employee database:
ArrayList List = new ArrayList();
// Adding an Employee to the database:
public void AddEmp(string name, string lname, decimal salary, bool status) {
List.Add(new Employee(name, lname, salary, status));
```