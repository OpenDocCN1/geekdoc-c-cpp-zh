print to output the employee’s type (e.g., "salaried employee:") followed by the rest of the employee’s information. Function `print` in the derived classes could also call earnings, even though earnings is a pure-virtual function in base class Employee.

The diagram in Fig. 20.8 shows each of the four classes in the hierarchy down the left side and functions earnings and print across the top. For each class, the diagram shows the desired results of each function. Italic text represents where the values from a particular object are used in the earnings and print functions. Class Employee specifies “= 0” for function earnings to indicate that this is a pure virtual function and hence has no implementation. Each derived class overrides this function to provide an appropriate implementation. We do not list base class Employee’s `get` and `set` functions because they’re not overridden in any of the derived classes—each of these functions is inherited and used “as is” by each of the derived classes.

|  | earnings | print |
|---|---|---|
| **Employee** | = 0 | *firstName lastName*<br>*social security number: SSN* |
| **Salaried-Employee** | *weeklySalary* | salaried employee: *firstName lastName*<br>social security number: *SSN*<br>weekly salary: *weeklySalary* |
| **Commission-Employee** | *commissionRate* × *grossSales* | commission employee: *firstName lastName*<br>social security number: *SSN*<br>gross sales: *grossSales*<br>commission rate: *commissionRate* |
| **BasePlus-Commission-Employee** | (*commissionRate* × *grossSales*) + *baseSalary* | base-salaried commission employee: *firstName lastName*<br>social security number: *SSN*<br>gross sales: *grossSales*<br>commission rate: *commissionRate*<br>base salary: *baseSalary* |

**Fig. 20.8**  |  Polymorphic interface for the Employee hierarchy classes.

# Employee Class Header

Let’s consider class Employee’s header (Fig. 20.9). The public member functions include a constructor that takes the first name, last name and social security number as arguments (lines 11–12); a virtual destructor (line 13); `set` functions that set the first name, last name and social security number (lines 15, 18 and 21, respectively); `get` functions that return the first name, last name and social security number (lines 16, 19 and 22, respectively); pure virtual function `earnings` (line 25) and virtual function `print` (line 26).

```
```cpp
// Fig. 20.9: Employee.h
// Employee abstract base class.
#ifndef EMPLOYEE_H
```
```

**Fig. 20.9**  |  Employee abstract base class. (Part 1 of 2.)