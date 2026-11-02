
![](img/d0d3b7423c2d9e5650be79209ea1885d_833_0.png)

**Fig. 20.18** | How virtual function calls work.

### CommissionEmployee Class *vtable*

The earnings function pointer in the *vtable* for class CommissionEmployee points to CommissionEmployee’s earnings function that returns the employee’s gross sales multiplied by the commission rate. The print function pointer points to the CommissionEmployee version of the function, which prints the employee’s type, name, social security number, commission rate and gross sales. As in class HourlyEmployee, both functions override the functions in class Employee.

### BasePlusCommissionEmployee Class vtable

The earnings function pointer in the vtable for class BasePlusCommissionEmployee points to the BasePlusCommissionEmployee's earnings function, which returns the employee's base salary plus gross sales multiplied by commission rate. The print function pointer points to the BasePlusCommissionEmployee version of the function, which prints the employee's base salary plus the type, name, social security number, commission rate and gross sales. Both functions override the functions in class CommissionEmployee.

### Inheriting Concrete virtual Functions

In our Employee case study, each concrete class provides its own implementation for virtual functions earnings and print. You've learned that each class which inherits directly from abstract base class Employee must implement earnings in order to be a concrete class, because earnings is a pure virtual function. These classes do not need to implement function print, however, to be considered concrete—print is not a pure virtual function and derived classes can inherit Employee's implementation of print. Furthermore, class BasePlusCommissionEmployee does not have to implement either function print or earnings—both function implementations can be inherited from concrete class CommissionEmployee. If a class in our hierarchy were to inherit function implementations in this manner, the vtable pointers for these functions would simply point to the function implementation that was being inherited. For example, if BasePlusCommissionEmployee did not override earnings, the earnings function pointer in the vtable for class BasePlusCommissionEmployee would point to the same earnings function as the vtable for class CommissionEmployee points to.

### Three Levels of Pointers to Implement Polymorphism

Polymorphism is accomplished through an elegant data structure involving three levels of pointers. We've discussed one level—the function pointers in the vtable. These point to the actual functions that execute when a virtual function is invoked.

Now we consider the second level of pointers. Whenever an object of a class with one or more virtual functions is instantiated, the compiler attaches to the object a pointer to the vtable for that class. This pointer is normally at the front of the object, but it isn't required to be implemented that way. In Fig. 20.18, these pointers are associated with the objects created in Fig. 20.17 (one object for each of the types SalariedEmployee, CommissionEmployee and BasePlusCommissionEmployee). The diagram displays each of the object's data member values. For example, the salariedEmployee object contains a pointer to the SalariedEmployee vtable; the object also contains the values John Smith, 111-11-1111 and $800.00.

The third level of pointers simply contains the handles to the objects that receive the virtual function calls. The handles in this level may also be references. Fig. 20.18 depicts the vector employees that contains Employee pointers. Now let's see how a typical virtual function call executes. Consider the call baseClassPtr->print() in function virtualViaPointer (line 69 of Fig. 20.17). Assume that baseClassPtr contains employees[1] (i.e., the address of object commissionEmployee in employees). When the compiler compiles this statement, it determines that the call is indeed being made via a base-class pointer and that print is a virtual function. The compiler determines that print is the second entry in each of the vtables. To locate this entry, the compiler notes that it will need to skip the first entry. Thus, the compiler compiles an offset or displacement into the table of machine-language object-code pointers to find the code that will execute the virtual function call. The size in bytes of the offset depends on the number of bytes used to represent a function pointer on an individual platform. For example, on a 32-bit platform, a pointer is typically stored in four bytes, whereas on a 64-bit platform, a pointer is typically stored in eight bytes. We assume four bytes for this discussion.

The compiler generates code that performs the following operations [Note: The numbers in the list correspond to the circled numbers in Fig. 20.18]:

- 1. Select the i-th entry of employees (in this case, the address of object commissionEmployee), and pass it as an argument to function virtualViaPointer. This sets parameter baseClassPtr to point to commissionEmployee.
- 2. Dereference that pointer to get to the commissionEmployee object—which, as you recall, begins with a pointer to the CommissionEmployee vtable.
- 3. Dereference commissionEmployee’s vtable pointer to get to the CommissionEmployee vtable.
- 4. Skip the offset of four bytes to select the print function pointer.
- 5. Dereference the print function pointer to form the “name” of the actual function to execute, and use the function call operator () to execute the appropriate print function, which in this case prints the employee’s type, name, social security number, gross sales and commission rate.

Fig. 20.18’s data structures may appear to be complex, but this complexity is managed by the compiler and hidden from you, making polymorphic programming straightforward. The pointer dereferencing operations and memory accesses that occur on every virtual function call require some additional execution time. The vtables and the vtable pointers added to the objects require some additional memory.

**Performance Tip 20.1**

Polymorphism, as typically implemented with virtual functions and dynamic binding in C++, is efficient. You can use these capabilities with nominal impact on performance.

**Performance Tip 20.2**

Virtual functions and dynamic binding enable polymorphic programming as an alternative to switch logic programming. Optimizing compilers normally generate polymorphic code that’s nearly as efficient as hand-coded switch-based logic. Polymorphism’s overhead is acceptable for most applications. In some situations—such as real-time applications with stringent performance requirements—polymorphism’s overhead may be too high.

## 20.8 Case Study: Payroll System Using Polymorphism and Runtime Type Information with Downcasting, dynamic_cast, typeid and type_info

Recall from the problem statement at the beginning of Section 20.6 that, for the current pay period, our fictitious company has decided to reward BasePlusCommissionEmployees by adding 10 percent to their base salaries. When processing Employee objects polymorphically in Section 20.6.5, we did not need to worry about the “specifics.” Now, however, to adjust the base salaries of BasePlusCommissionEmployees, we have to determine the specific type of each Employee object at execution time, then act appropriately. This section demonstrates the powerful capabilities of runtime type information (RTTI) and dynamic casting, which enable a program to determine an object's type at execution time and act on that object accordingly.

Figure 20.19 uses the Employee hierarchy developed in Section 20.6 and increases by 10 percent the base salary of each BasePlusCommissionEmployee. Line 21 declares three-element vector employees that stores pointers to Employee objects. Lines 24–29 populate the vector with the addresses of dynamically allocated objects of classes SalariedEmployee (Figs. 20.11–20.12), CommissionEmployee (Figs. 20.13–20.14) and BasePlusCommissionEmployee (Figs. 20.15–20.16). Lines 32–52 iterate through the employees vector and display each Employee's information by invoking member function print (line 34). Recall that because print is declared virtual in base class Employee, the system invokes the appropriate derived-class object's print function.

```cpp
1  // Fig. 20.19: fig20_19.cpp
2  // Demonstrating downcasting and runtime type information.
3  // NOTE: You may need to enable RTTI on your compiler
4  // before you can compile this application.
5  #include <iostream>
6  #include <iomanip>
7  #include <vector>
8  
9  #include <typeinfo>
10 #include "Employee.h"
11 #include "SalariedEmployee.h"
12 #include "CommissionEmployee.h"
13 #include "BasePlusCommissionEmployee.h"
14 using namespace std;
15 
16 int main()
17 {
18     // set floating-point output formatting
19     cout << fixed << setprecision( 2 );
20 
21     // create vector of three base-class pointers
22     vector < Employee * > employees( 3 );
23 
24     // initialize vector with various kinds of Employees
25     employees[ 0 ] = new SalariedEmployee(
26         "John", "Smith", "111-11-1111", 800 );
27     employees[ 1 ] = new CommissionEmployee(
28         "Sue", "Jones", "333-33-3333", 10000, .06 );
29     employees[ 2 ] = new BasePlusCommissionEmployee(
30         "Bob", "Lewis", "444-44-4444", 5000, .04, 300 );
```

**Fig. 20.19** | Demonstrating downcasting and runtime type information. (Part 1 of 2.)

1. Some compilers require that RTTI be enabled before it can be used in a program. The compilers we used for testing this book's C++ examples—GNU C++, Visual C++ and Xcode LLVM—each enable RTTI by default.
