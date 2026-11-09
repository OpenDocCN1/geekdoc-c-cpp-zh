![](bbox=[0.177, 0.064, 0.763, 0.387])

```
```c
void M3() {
    Employee e;
    Int32 year;
    e = new Manager();
    e = Employee.Lookup("Joe");
    year = e.GetYearsEmployed();
    e.GetProgressReport();
}
```
```

FIGURE 4-10 Employee’s static Lookup method allocates and initializes a Manager object for Joe.

![](bbox=[0.177, 0.434, 0.763, 0.742])

```
```c
void M3() {
    Employee e;
    Int32 year;
    e = new Manager();
    e = Employee.Lookup("Joe");
    year = e.GetYearsEmployed();
    e.GetProgressReport();
}
```
```

FIGURE 4-11 Employee’s nonvirtual instance GetYearsEmployed method is called, returning 5.

The next line of code in M3 calls Employee’s virtual instance GetProgressReport method. When calling a virtual instance method, the JIT compiler produces some additional code in the method, which will be executed each time the method is invoked. This code will first look in the variable being used to make the call and then follow the address to the calling object. In this case, the variable e points to the Manager object representing “Joe.” Then, the code will examine the object’s internal type