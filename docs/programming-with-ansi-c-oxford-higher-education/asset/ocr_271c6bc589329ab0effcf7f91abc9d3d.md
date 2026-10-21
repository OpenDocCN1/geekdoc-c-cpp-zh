```
void DisplayDetails()
{
    cout << EmpID << "\n";
    cout << Name << "\n";
    cout << Designation << "\n";
    cout << Department << "\n";
    cout << Salary << "\n";
}
};

void main()
{
    employee Robin;
    Robin.InsertDetails();
    Robin.DisplayDetails();
}
```

> Note When we define a class and define its data members without writing them under any access specifier, they are treated as private by default.

# How the Program Works

If this program is slightly modified by replacing the fourth line class employee by struct employee, the program works just the same. However, there is a difference, which is not visible at the moment. Add the following line in both the programs (with employee as a class in the first program and as a structure in the second program). The main function is now different as follows:

```
void main()
{
    employee Robin;
    Robin.InsertDetails();
    Robin.DisplayDetails();
    // The following line is added
    Robin.EmpID = 10;
    /* This line will not be compiled in the case of class,
    but it will work fine in a structure */
}
```

The first program is not compiled, but the second one is. The default behaviour in the struct definition is different. An attribute without an access specifier name is treated as public in structure unlike private in class. Here, EmpID in the first program is private whereas in the second it is public. It can be accessed by the second program’s statement but not by that of the first program and hence the second program is compiled. It is not difficult to understand why default is private in a class. Unless explicitly specified (i.e., defined under public), anything defined should be considered private in a class.

It might seem illogical to have the structure which behaves in the same manner as a class, except one seemingly insignificant difference in the default data type. The reason for such behaviour of a structure lies in backward compatibility with C. Consider the following code borrowed from C:

```
struct Evaluator
{
```

> In the case of a class, the data members and member functions are private by default (unless declared otherwise), whereas in the case of a structure, the entities are public by default.