# 11.2 Base Classes and Derived Classes

**Figure 11.1** lists several simple examples of base classes and derived classes. Base classes tend to be *more general* and derived classes tend to be *more specific*.

# **Fig. 11.1 Inheritance examples.**

| Base class | Derived classes |
|---|---|
| `Student` | `GraduateStudent`, `UndergraduateStudent` |
| `Shape` | `Circle`, `Triangle`, `Rectangle`, `Sphere`, `Cube` |
| `Loan` | `CarLoan`, `HomeImprovementLoan`, `MortgageLoan` |
| `Employee` | `Faculty`, `Staff` |
| `Account` | `CheckingAccount`, `SavingsAccount` |

Because every derived-class object is *an* object of its base class, and one base class can have *many* derived classes, the set of objects represented by a base class typically is *larger* than the set of objects represented by any of its derived classes. For example, the base class `Vehicle` represents all vehicles, including cars, trucks, boats,