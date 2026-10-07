8. Enter employee.cpp, which can be found on the following pages. Notice that we can make an entire struct a friend of another struct. All the member functions of accountant have access to private elements of employee.

a) Create struct accountant in the file employee.cpp. Within the struct, declare a function payroll() which shows an employee object passed by value into the payroll() function. Submit the code.

b) Define the payroll() function which accesses and prints the private information about employee. Simply select them as if they were public members of the struct. Convince yourself that you can compile the code. Submit the code.

c) To show this isn't normally possible, comment out the friend declaration in the employee struct. What happens when you compile? Submit the code.

d) Create a new struct called boss with a member function called seepage(employee). This should precede the employee declaration. To do this, you must first tell the compiler there is a struct somewhere called employee with a name declaration:

```
struct employee;
```

Submit the code.

e) A type name declaration has no body, so the compiler knows the name exists, but not how big it is. Now create a declaration inside struct employee which says "the seepage() function of struct boss has friend status, but only that function.\ Submit the code.

f) See if you can change the friend declaration in struct employee so it only gives access to accountant::payroll(), and not the entire struct accountant. Submit the code.