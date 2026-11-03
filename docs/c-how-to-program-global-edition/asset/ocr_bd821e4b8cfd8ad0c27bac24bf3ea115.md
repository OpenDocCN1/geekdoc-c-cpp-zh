![](bbox=[0.05, 0.07, 0.95, 0.86])

# Flow of Virtual Function Call baseClassPtr->print()

When baseClassPtr Points to Object commissionEmployee

# Fig. 20.18 | How virtual function calls work.

# CommissionEmployee Class vtable

The earnings function pointer in the vtable for class CommissionEmployee points to CommissionEmployee's earnings function that returns the employee's gross sales multiplied by the commission rate. The print function pointer points to the CommissionEmployee version of the function, which prints the employee's type, name, social security number, commission rate and gross sales. As in class HourlyEmployee, both functions override the functions in class Employee.