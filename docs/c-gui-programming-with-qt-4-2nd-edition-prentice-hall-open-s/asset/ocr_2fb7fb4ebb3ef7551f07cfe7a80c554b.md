departments and employees.
The EmployeeForm class provides a drill-down from the main form's summary of employees to a particular employee's details. When invoked, the form shows the specified employee if a valid employee ID is given, or the first employee otherwise. (The form is shown in Figure 13.3.) Users can navigate through the employees, edit or delete existing employees, and add new employees.

# Figure 13.3. The Employee dialog

![](bbox=[0.019, 0.203, 0.559, 0.499])

We have provided the following enum in employeeform.h to give meaningful names to the column indexes:

```
enum {
    Employee_Id = 0,
    Employee_Name = 1,
    Employee_DepartmentId = 2,
    Employee_Extension = 3,
    Employee_Email = 4,
    Employee_StartDate = 5
};
```

The rest of the header file defines the EmployeeForm class:

```
class EmployeeForm : public QDialog
{
    Q_OBJECT
public:
    EmployeeForm(int id, QWidget *parent = 0);
```