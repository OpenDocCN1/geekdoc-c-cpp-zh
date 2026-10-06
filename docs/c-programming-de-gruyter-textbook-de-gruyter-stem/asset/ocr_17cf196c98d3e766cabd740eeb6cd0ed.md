# 190 5 Data Sharing and Protecting

...

```
#endif
```

In this header file, the compiler first needs to judge whether the identifier HEAD_H has been defined or not. If it has not been defined, the header file should not have been compiled yet, and the compiler will macrodefine the identifier HEAD_H and compile the following program segment. The defined identifier marks that the file has already been compiled; if the identifier has been deined, then the file should have been compiled, and the compiler will not recompile the following program segment anymore. In this way, we can avoid the redefinition of class Point.

# 5.7 Example – Personnel Information Management Program

We have used a personnel information management program for a small company in Chapter 4 as an example to explain the design and use of classes and member functions. In this section we will do the following improvements to Example 4.5 from the last chapter:

+   1. We have introduced static data members in Section 5.2.1 and 5.3.1 In this example we will use the property that a static data member has a static lifetime to focus a data member – the number of employees. This new functionality is: add a static data member in employee to store the currently maximum employee number, and the currently maximum will increase automatically when adding a new employee. Through this, we can avoid the problem of frequently calling the member function IncreaseEmpNo (int steps).
2. We have introduced the general structure of C++ programs in Section 5.6.1. Here we will adjust the program structure based on Example 4,5 in the last chapter: we will divide the definition part and implementation part of class employee into two files.

The design class in this example is almost the same as the one in Example 4.5. Expect that we add a static data member static employeeNo in the base class employee to store the currently maximum employee number; we also delete the member function

| employee |
| # individualEmpNo : int |
| # grade : int |
| # accumPay : float |
| # employeeNo : int = 1000 |
| + employee() |
| ~employee() |
| + promote(int) : void void |
| + SetaccumPay(pe : float) : void |
| GetIndividualEmpNo() : int |
| + Grade() : int |
| + GetaccumPay() : float |

> Fig. 5.9: UML diagram of personnel information management program.