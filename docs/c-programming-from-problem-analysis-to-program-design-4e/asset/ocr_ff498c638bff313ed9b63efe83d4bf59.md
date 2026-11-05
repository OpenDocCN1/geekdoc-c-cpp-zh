classes. This enables other applications to use the Employee class. Actual checks for the XYZ JobSource temp agency may need to be printed, payroll records saved, and other reports generated. By separating the logic from the design of the GUI presentation, the Employee class can be reused for many other applications.

# DATA

Table 9-9 lists the data field members needed for the Employee class. In addition to these entered values, instance variables to store deductions and pay amounts are needed.

**TABLE 9-9** Instance field members for the Employee class

| Data description | Type | Identifier |
|---|---|---|
| Employee last name | `string` | `employeeLastName` |
| Employee first name | `string` | `employeeFirstName` |
| Number of dependents | `int` | `noOfDependents` |
| Number of hours worked | `double` | `noOfHours` |

# CONSTANTS

For this example, several values such as hourly rate, Social Security, and federal withholding tax rates are the same for all employees. The user does not have to enter these values at run time; instead, constants can be defined for the values in the Employee class in the methods that use their values. Any objects instantiated of that class can then have access to the amounts, as shown in Table 9-10.

**TABLE 9-10** Constant field members for the Employee class

| Data description | Type | Identifier | Value |
|---|---|---|---|
| Hourly rate | `double` | `RATE` | 150.00 |
| Federal tax deduction percentage | `double` | `FEDERAL_TAX` | 0.25 |
| Social Security deduction percentage | `double` | `SOCIAL_SECURITY_RATE` | 0.0785 |
| Dependent allowance percentage | `double` | `DEPENDENT_ALLOWANCE` | 0.0575 |
| Agency fee for the contract | `double` | `AGENCY_CHARGE` | 0.13 |