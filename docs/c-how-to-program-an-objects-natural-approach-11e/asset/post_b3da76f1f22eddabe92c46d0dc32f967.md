
```cpp
// output each Employee
std::cout << "EMPLOYEES PROCESSED INDIVIDUALLY VIA VARIABLE NAMES\n"
          << std::format("{}\n{}\n{}\n{}\n",
                         salaried.toString(), "earned $", salaried.earnings(),
                         commission.toString(), "earned $", commission.earnings());

// create and initialize vector of base-class pointers
std::vector<Employee*> employees{&salaried, &commission};

std::cout << "EMPLOYEES PROCESSED POLYMORPHICALLY VIA"
          << " DYNAMIC BINDING\n\n";

// call virtualViaPointer to print each Employee
// and earnings using dynamic binding
std::cout << "VIRTUAL FUNCTION CALLS MADE VIA BASE-CLASS POINTERS\n";

for (const Employee* employeePtr : employees) {
    virtualViaPointer(employeePtr);
}

// call virtualViaReference to print each Employee
// and earnings using dynamic binding
std::cout << "VIRTUAL FUNCTION CALLS MADE VIA BASE-CLASS REFERENCES\n";

for (const Employee* employeePtr : employees) {
    virtualViaReference(*employeePtr); // note dereferenced pointer
}

// call Employee virtual functions toString and earnings via a
// base-class pointer using dynamic binding
void virtualViaPointer(const Employee* baseClassPtr) {
    std::cout << std::format("{}\nearned ${:.2f}\n",
                             baseClassPtr->toString(), baseClassPtr->earnings());
}

// call Employee virtual functions toString and earnings via a
// base-class reference using dynamic binding
void virtualViaReference(const Employee& baseClassRef) {
    std::cout << std::format("{}\nearned ${:.2f}\n",
                             baseClassRef.toString(), baseClassRef.earnings());
}
```

![](img/7b5e2088e71c7f78681d4ddbcf104c06_626_0.png)

**Fig. 10.17** | Processing Employee derived-class objects with variable-name handles then polymorphically using base-class pointers and references. (Part 2 of 3.)

## KIMI K2 与 DeepSeek V3 跑分对比

Kimi K2 是月之暗面推出的大模型，其能力完全对标 OpenAI o1 正式版，因此我们选择 DeepSeek V3 作为主要对比对象。

| 评测集 | 模型 | 分数 |
| --- | --- | --- |
| MATH-500 (数学) | Kimi K2 | 96.5 |
|  | DeepSeek V3 | 90.2 |
| AIME'24/MATH-500 (数学竞赛) | Kimi K2 | 60.0 |
|  | DeepSeek V3 | 39.4 |
| Codeforces (编程竞赛) | Kimi K2 | 163.0 |
|  | DeepSeek V3 | 171.0 |
| SWE-bench Verified (编程实战) | Kimi K2 | 65.8 |
|  | DeepSeek V3 | 42.0 |
| Aider Polyglot (编程语言) | Kimi K2 | 69.0 |
|  | DeepSeek V3 | 47.0 |
| GPQA Diamond (科学) | Kimi K2 | 67.4 |
|  | DeepSeek V3 | 59.1 |
| MMMLU (综合知识) | Kimi K2 | 55.2 |
|  | DeepSeek V3 | 46.6 |
| H-MMLU (综合知识) | Kimi K2 | 64.7 |
|  | DeepSeek V3 | 58.3 |
| MMMLU-Pro (综合知识) | Kimi K2 | 64.2 |
|  | DeepSeek V3 | 67.2 |

注：以上数据来源于官方公开的评测结果，实际效果可能因场景而异。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_629_0.png)

**Fig. 10.18** | How virtual function calls work.

### Employee Class vtable

The first function pointer in the Employee class vtable is set to 0 (i.e., nullptr) because earnings is a pure virtual function with no implementation. The second points to toString, which returns a string containing the employee’s name. We’ve abbreviated each toString function’s output in this figure to conserve space—note the pointers in the vtables actually point to each function’s code. Any class with one or more pure virtual functions (represented with the value 0) in its vtable is an abstract class. SalariedEmployee and CommissionEmployee are concrete classes—they have no nullptrs in their vtables.

### SalariedEmployee Class vtable

The earnings function pointer in the SalariedEmployee vtable points to that class’s override of the earnings function, which returns the salary. SalariedEmployee also overrides toString, so the corresponding function pointer points to SalariedEmployee’s toString function, which returns the employee’s name and salary.

### CommissionEmployee Class vtable

The earnings function pointer in the CommissionEmployee *vtable* points to the CommissionEmployee’s earnings function, which returns the employee’s gross sales multiplied by the commission rate. The toString function pointer points to the CommissionEmployee version of the function, which returns the employee’s name, commission rate and gross sales. As in class SalariedEmployee, both functions override class Employee’s functions.

### Inheriting Concrete virtual Functions

Each concrete class in our Employee case study provides virtual earnings and toString implementations. You’ve learned that because earnings is a pure virtual function, each direct derived class of Employee must implement earnings to be a concrete class. Direct derived classes do not need to implement toString to be considered concrete. They can inherit class Employee’s toString implementation. In our case, both derived classes override Employee’s toString.

If a derived class were to inherit toString and not override it, this function’s *vtable* pointer would point to the inherited implementation. For example, if CommissionEmployee did not override toString, CommissionEmployee’s toString function pointer in the *vtable* would point to the same toString function as in class Employee’s *vtable*.

### Three Levels of Pointers to Implement Runtime Polymorphism

Runtime polymorphism can be accomplished through an elegant data structure involving three levels of pointers. We’ve discussed one level—the function pointers in the *vtable*. These point to the functions that execute when a virtual function is invoked.

Now we consider the second level of pointers. **Whenever an object with one or more virtual functions is instantiated, the compiler attaches to each object a pointer to the class’s *vtable*.** This pointer is usually at the front of the object, but it isn’t required to be implemented that way. In the *vtable* diagram, these pointers are associated with the SalariedEmployee and CommissionEmployee objects defined in Fig. 10.17. The diagram shows each object’s data member values.

The third level of pointers contains the addresses of the objects on which the virtual functions will be called. The *vtable* diagram’s rightmost column depicts the vector employees containing these Employee pointers.

Now let’s see how a typical virtual function call executes. Consider in the function virtualViaPointer the call **baseClassPtr->toString()** (Fig. 10.17, line 52). Assume that baseClassPtr contains employees[1], commission’s address in employees. When this statement is compiled, the compiler sees that the call is made via a base-class pointer and that toString is a virtual function. The compiler sees that toString is the second entry in each *vtable*. So it includes an offset into the table of machine-language object-code pointers to find the code that will execute the virtual function call.

The compiler generates code that performs the following operations—the numbers in the list correspond to the circled numbers in Fig. 10.18:

- 1. Select the *ith* employee’s entry—the commission object’s address—and pass it as an argument to function virtualViaPointer. This aims the baseClassPtr parameter at the commission object.
- 2. Dereference that pointer to access the commission object, which begins with a pointer to class CommissionEmployee’s *vtable*.
- 3. Dereference the *vtable* pointer to access class `CommissionEmployee`’s *vtable*.
- 4. Skip the offset to select the `toString` function pointer.¹⁸
- 5. Execute `toString` for the `commission` object, returning a string containing the employee’s name, gross sales and commission rate.

The *vtable* diagram’s data structures may appear complex. **The compiler hides this complexity from you**, making runtime polymorphic programming straightforward. The pointer dereferencing operations and memory accesses for each `virtual` function call require additional execution time. The *vtables* and *vtable* pointers added to the objects require some additional memory.

**Runtime polymorphism is efficient, as typically implemented with `virtual` functions and dynamic binding in C++.** For most applications, you can use these capabilities with nominal impact on execution performance and memory consumption. In some situations, polymorphism’s overhead may be too high—such as in real-time applications with stringent execution-timing performance requirements or in an application with an enormous number of *small* objects in which the size of the *vtable* pointer is large when compared to each object’s size.

### Checkpoint

- 1. (*True/False*) The overhead of runtime polymorphism—in terms of additional memory consumption and processor time—is insignificant, so you should feel free to use it in your applications.  
  **Answer:** False. Actually, understanding the overhead of runtime polymorphism—in terms of additional memory consumption and processor time—can help you determine when to use runtime polymorphism in your applications and when to avoid it.
- 2. (*Fill-in*) When C++ compiles a class with one or more `virtual` functions, it builds a ______ for that class. This contains pointers to the class’s `virtual` functions.  
  **Answer:** virtual function table (*vtable*)
- 3. (*True/False*) The *vtable* diagram’s complexity discourages programmers from doing polymorphic programming.  
  **Answer:** False. Actually, although the *vtable* diagram’s data structures may appear complex, the compiler hides this complexity from you, making runtime polymorphic programming straightforward.

## 10.11 **Program to an Interface, Not an Implementation**¹⁹

Implementation inheritance is primarily used to define closely related classes with many of the same data members and member function implementations. This kind of inheritance creates tightly coupled classes in which the base class’s data members and member functions are inherited into derived classes. Changes to a base class directly affect all corresponding derived classes.

- 18. In practice, Steps 3 and 4 can be implemented as a single machine instruction.
- 19. Defined in Gamma et al., pp. 17–18; also discussed in Joshua Bloch, *Effective Java*. Upper Saddle River, NJ: Addison-Wesley, 2008.
