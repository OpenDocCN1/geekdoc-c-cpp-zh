# Figure 15.1 A pointer to an Account object

![](bbox=[0.25, 0.16, 0.68, 0.34])

```
* (p.x) = 253.7; // Error
```

The variable p is not a Point object, but a pointer to a Point object, so it must be dereferenced with the * operator before applying the . operator. C++ provides a simpler syntax to access fields of an object through a pointer. The pointer operator eliminates the need for the parentheses:

```
Point *p = new Point;
p->x = 253.7;
p->y = -00.5;
```

The pair of symbols -> constitute one operator (no space in between is allowed), and the operator is meant to look like an arrow pointing right. There is no associated left pointing arrow in C++.

You can use the -> operator to access the methods of an object referenced by a pointer:

```
Account *acct_ptr = new Account("Joe", 400, 1300.00);
if (acct_ptr->withdraw(10.00))
    std::cout << "Withdrawal successful\\n";
else
    std::cout << "*** Insufficient funds ***\\n";
```

An executing program will not automatically deallocate the memory allocated via new. It is the programmer's responsibility to manually deallocate the memory when the object is no longer needed. The delete operator with no [] decoration frees up a single dynamically allocated object:

```
// acct_ptr points to an Account object previously allocated
// via new
delete acct_ptr;
```

The following function has a logic error because it fails to free up memory allocated with new:

```
void faulty_func() {
    Account *acct_ptr = new Account("Joe", 400, 1300.00);
    if (acct_ptr->withdraw(10.00))
        std::cout << "Withdrawal successful\\n";
    else
```