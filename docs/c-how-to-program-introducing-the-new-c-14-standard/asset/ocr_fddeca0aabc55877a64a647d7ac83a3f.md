A widely accepted practice to minimize the proliferation of identifier names is to use the same name for a set function’s parameter and the data member it sets, and to reference the data member in the set function’s body via `this->`.

# *Type of the `this` Pointer*

The type of the `this` pointer depends on the type of the object and whether the member function in which `this` is used is declared `const`:

+   - In a non-`const` member function of class `Employee`, the `this` pointer has the type `Employee* const`—a constant pointer to a *nonconstant* Employee.
+   - In a `const` member function, `this` has the type `const Employee* const`—a constant pointer to a *constant* Employee.