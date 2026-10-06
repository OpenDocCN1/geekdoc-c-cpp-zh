306 - 7 Inheritance and Derivation

![](bbox=[0.176, 0.083, 0.824, 0.558])

**Fig. 7.10:** UML of personnel information management system of a small corporation.

# 7.7.3 Source Code and Explanation

**Example 7.10:** Personnel information management system.
The entire program is divided into three files: *employee.h* is a header file for class definitions; *employee.cpp* is a file in which functions of the classes are implemented; and *7_10.cpp* contains the main function `main()`. After compiling, *7_10.cpp* and *employee.cpp* are linked together. In the VC++ development environment, they should be placed in one project.

```
//employee.h
class employee
{
protected:
    char name[20];
    int individualEmpNo;
    //name
//employee number
```