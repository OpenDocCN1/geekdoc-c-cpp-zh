# 12.3 Relationships Among Objects
in an Inheritance Hierarchy

**Section 11.3** created an employee class hierarchy, in which class `BasePlusCommissionEmployee` inherited from class `CommissionEmployee`. The **Chapter 11** examples manipulated `CommissionEmployee` and `BasePlusCommissionEmployee` objects by using the objects’ names to invoke their member functions. We now examine the relationships among classes in a hierarchy more closely. The next several sections present a series of examples that demonstrate how base-class and derived-class *pointers* can be aimed at base-class and derived-class objects, and how those pointers can be used to invoke member functions that manipulate those objects.

+   - In **Section 12.3.1**, we assign the address of a derived-class object to a base-class pointer, then show that invoking a function via the base-class pointer invokes the *base-class* functionality in the derived-class object—i.e., the *type* of the *handle* determines which *function* is called.
+   - In **Section 12.3.2**, we assign the address of a base-class object to a derived-class pointer, which results in a compilation error. We discuss the error message and investigate why the compiler does not allow such an assignment.
+   - In **Section 12.3.3**, we assign the address of a derived-class object to a base-class pointer, then examine how the base-class pointer