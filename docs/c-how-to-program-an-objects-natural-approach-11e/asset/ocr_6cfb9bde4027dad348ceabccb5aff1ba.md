Employee is a PhoneNumber. However, an Employee has a BirthDate and has a Phone-\nNumber.

It’s possible to treat base-class objects and derived-class objects similarly—their\ncommonalities are expressed in the base-class members. Later in this chapter, we’ll con-\nsider examples that take advantage of that relationship.

# Checkpoint

+   1. **(True/False)** With public inheritance, the derived class can manipulate private\n   base-class members through inherited base-class public and protected member func-\n   tions—if these base-class member functions provide such functionality.\n   **Answer:** True.

+   2. **(Fill-in)** The commonalities between base-class and derived-class objects are\n   expressed in the __________.\n   **Answer:** base-class members.

+   3. **(Code)** Write the header of a class definition that would indicate class Square is a sub-\n   class of TwoDimensionalShape.\n   **Answer:** `class Square : public TwoDimensionalShape`

# 10.3  Relationship Between Base and Derived Classes

This section uses an inheritance hierarchy of employee types in a company’s payroll appli-\ncation to demonstrate the relationship between base and derived classes:

+   - Base-class salaried employees are paid a fixed weekly salary.\n- Derived-class salaried commission employees receive a weekly salary *plus* a per-\n  centage of their sales.

# 10.3.1 Creating and Using a SalariedEmployee Class

Let’s examine SalariedEmployee’s class definition (Figs. 10.1–10.2). Its header\n(Fig. 10.1) specifies the class’s public services:

+   - a constructor (line 9),\n- member function earnings (line 17),\n- member function toString (line 18) and\n- public set and get functions that manipulate the class’s data members m_name and\n  m_salary (declared in lines 20–21).

Member function setSalary’s implementation (Fig. 10.2, lines 22–28) validates its argu-\nment before modifying the data member m_salary.

```
1  // Fig. 10.1: SalariedEmployee.h\n2  // SalariedEmployee class definition.\n3  #pragma once // prevent multiple inclusions of header
```

**Fig. 10.1**  |  SalariedEmployee class definition. (Part 1 of 2.)