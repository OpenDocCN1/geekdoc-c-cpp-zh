
Classes without any `nullptr`s in their *vtables* (such as `SalariedEmployee`, `CommissionEmployee` and `BasePlusCommissionEmployee`) are *concrete* classes.

### `SalariedEmployee` *Class vtable*

Class `SalariedEmployee` overrides function `earnings` to return the employee’s weekly salary, so the function pointer points to the `earnings` function of class `SalariedEmployee`. `SalariedEmployee` also overrides `toString`, so the corresponding function pointer points to the `SalariedEmployee` member function that returns `"salaried employee: "` followed by the employee’s name, social security number and weekly salary.

### `CommissionEmployee` *Class vtable*

The `earnings` function pointer in the *vtable* for class `CommissionEmployee` points to the `CommissionEmployee`’s `earnings` function that returns the employee’s gross sales multiplied by the commission rate. The `toString` function pointer points to the `CommissionEmployee` version of the function, which returns the employee’s type, name, social security number, commission rate and gross sales. As in class `SalariedEmployee`, both functions override the functions in class `Employee`.

### `BasePlusCommissionEmployee` Class *vtable*

The `earnings` function pointer in the *vtable* for class `BasePlusCommissionEmployee` points to the `BasePlusCommissionEmployee`’s `earnings` function, which returns the employee’s base salary plus gross sales multiplied by commission rate. The `toString` function pointer points to the `BasePlusCommissionEmployee` version of the function, which returns the employee’s base salary plus the type, name, social security number, commission rate and gross sales. Both functions override the functions in class `CommissionEmployee`.

### *Inheriting Concrete* `virtual` *Functions*

In our `Employee` case study, each *concrete* class provides its own implementation for `virtual` functions `earnings` and `toString`. You’ve learned that each class that inherits *directly* from abstract base class `Employee` *must implement* `earnings` in order to be a *concrete* class, because `earnings` is a pure `virtual` function. These classes do *not* need to implement function `toString`, however, to be considered concrete—`toString` is *not* a pure `virtual` function and derived classes can inherit class `Employee`’s implementation of `toString`.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1622_0.png)

Fig. 12.18 How `virtual` function calls work.

Furthermore, class `BasePlusCommissionEmployee` does *not* have to implement either function `toString` or `earnings`—both function implementations can be inherited from concrete class `CommissionEmployee`. If a class in our hierarchy were to inherit function implementations in this manner, the *vtable* pointers for these functions would simply point to the function implementation that was being inherited. For example, if `BasePlusCommissionEmployee` did not override `earnings`, the `earnings` function pointer in the *vtable* for class `BasePlusCommissionEmployee` would point to the same `earnings` function as the *vtable* for class `CommissionEmployee`.

### *Three Levels of Pointers to Implement Polymorphism*

Polymorphism is accomplished through an elegant data structure involving *three levels of pointers*. We’ve discussed one level—the function pointers in the *vtable*. These point to the actual functions that execute when a `virtual` function is invoked.

Now we consider the second level of pointers. *Whenever an object of a class with one or more `virtual` functions is instantiated, the compiler attaches to the object a pointer to the vtable for that class.* This pointer is normally at the front of the object, but it isn’t required to be implemented that way. In **Fig. 12.18**, these pointers are associated with the objects created in **Fig. 12.17** (one object for each of the types `SalariedEmployee`, `CommissionEmployee` and `BasePlusCommissionEmployee`). The diagram shows each of the object’s data member values. For example, the `salariedEmployee` object contains a pointer to the `SalariedEmployee` *vtable*; the object also contains the values `John Smith`, `111-11-1111` and `$800.00`.

The third level of pointers simply contains the handles to the objects that receive the `virtual` function calls. The handles in this level may also be *references*. **Figure 12.18** depicts the `vector` `employees` that contains *Employee pointers*.

Now let’s see how a typical `virtual` function call executes. Consider in the function `virtualViaPointer` the call `baseClassPtr->toString()` (line 62 of **Fig. 12.17**). Assume that `baseClassPtr` contains `employees[1]` (i.e., the address of object `commissionEmployee` in `employees`). When the compiler compiles this statement, it determines that the call is indeed being made via a *base-class pointer* and that `toString` is a `virtual` function.

The compiler determines that `toString` is the *second entry* in each of the *vtables*. To locate this entry, the compiler notes that it will need to skip the first entry. Thus, the compiler compiles an **offset** or **displacement** into the table of machine-language object-code pointers to find the code that will execute the `virtual` function call. The size in bytes of the offset depends on the number of bytes used to represent a function pointer on an individual platform. For example, on a 32-bit platform, a pointer is typically stored in four bytes, whereas on a 64-bit platform, a pointer is typically stored in eight bytes. We assume four bytes for this discussion.

The compiler generates code that performs the following operations [*Note:* The numbers in the list correspond to the circled numbers in **Fig. 12.18**]:

- 1. Select the *i*th entry of `employees` (in this case, the address of object `CommissionEmployee`) and pass it as an argument to function `virtualViaPointer`. This sets parameter `baseClassPtr` to point to `commissionEmployee`.
- 2. *Dereference* that pointer to get to the `commissionEmployee` object—which, as you recall, begins with a pointer to the `CommissionEmployee` *vtable*.
- 3. *Dereference* `commissionEmployee`’s vtable pointer to get to the `CommissionEmployee` *vtable*.
- 4. Skip the offset of four bytes to select the `toString` function pointer.
- 5. *Dereference* the `toString` function pointer to form the “name” of the actual function to execute, and use the function-call operator `()` to execute the appropriate `toString` function, which in this case returns the employee’s type, name, social security number, gross sales and commission rate.

**Figure 12.18**’s data structures may appear complex, but this complexity is managed by the compiler and *hidden* from you, making polymorphic programming straightforward. The pointer dereferencing operations and memory accesses that occur on every `virtual` function call require some additional execution time. The *vtables* and the *vtable* pointers added to the objects require some additional memory.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1626_0.png)

### Performance Tip 12.1

*Polymorphism, as typically implemented with `virtual` functions and dynamic binding in C++, is efficient. For most applications, you can use these capabilities with nominal impact on performance.*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1626_1.png)

### Performance Tip 12.2

*Virtual functions and dynamic binding enable polymorphic programming as an alternative to `switch` logic programming. Optimizing compilers normally generate polymorphic code that’s nearly as efficient as hand-coded `switch`-based logic. Polymorphism’s overhead is acceptable for most applications. In some situations—such as real-time applications with stringent performance requirements—polymorphism’s overhead may be too high.*

## 12.9 Case Study: Payroll System Using Polymorphism and Runtime Type Information with Downcasting, `dynamic_cast`, `typeid` and `type_info`

Recall from the problem statement at the beginning of **Section 12.7** that, for the current pay period, our fictitious company has decided to reward `BasePlusCommissionEmployees` by adding 10 percent to their base salaries. When processing `Employee` objects polymorphically in **Section 12.7.5**, we did not need to worry about the “specifics.” Now, however, to adjust the base salaries of `BasePlusCommissionEmployees`, we have to determine the *specific type* of each `Employee` object *at execution time*, then act appropriately. This section demonstrates the powerful capabilities of **runtime type information (RTTI)** and **dynamic casting**, which enable a program to determine an object’s type at execution time and act on that object accordingly.^1

1. Some compilers require that RTTI be enabled before it can be used in a program. The compilers we used for testing this book’s examples
