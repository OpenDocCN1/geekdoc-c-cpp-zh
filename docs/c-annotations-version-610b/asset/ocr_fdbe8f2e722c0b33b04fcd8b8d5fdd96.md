# 16.3. USING POINTERS TO MEMBERS

```
```cpp
object.*valuePtr = 12345;                 // (2)
cout << object.*valuePtr << '\n' <<
        object.d_value << '\n';

ptr->*valuePtr = 54321;                     // (3)
cout << object.d_value << '\n' <<
        (object.*getPtr()) << '\n' <<      // (4)
        (ptr->*getPtr()) << '\n';
}
```
```

We note:

+   - At (1) a `PointerDemo` object and a pointer to such an object is defined.
+   - At (2) we specify an object (and hence the `.*` operator) to reach the member `valuePtr` points to. This member is given a value.
+   - At (3) the same member is assigned another value, but this time using the pointer to a `PointerDemo` object. Hence we use the `->*` operator.
+   - At (4) the `.*` and `->*` are used once again, this time to call a function through a pointer to member. As the function argument list has a higher priority than the pointer to member field selector operator, the latter *must be protected by parentheses*.

Pointers to members can be used profitably in situations where a class has a member that behaves differently depending on a configuration setting. Consider once again the class `Person` from section [9.3](#). `Person` defines data members holding a person’s name, address and phone number. Assume we want to construct a `Person` database of employees. The employee database can be queried, but depending on the kind of person querying the database either the name, the name and phone number or all stored information about the person is made available. This implies that a member function like `address` must return something like `<not available>` in cases where the person querying the database is not allowed to see the person’s address, and the actual address in other cases.

The employee database is opened specifying as an argument reflecting the status of the employee who wants to make some queries. The status could reflect his or her position in the organization, like BOARD, SUPERVISOR, SALESPERSON, or CLERK. The first two categories are allowed to see all information about the employees, a SALESPERSON is allowed to see the employee’s phone numbers, while the CLERK is only allowed to verify whether a person is actually a member of the organization.

We now construct a member string `personInfo(char const *name)` in the database class. A standard implementation of this class could be:

```
```cpp
string PersonData::personInfo(char const *name)
{
    Person *p = lookup(name);   // see if ‘name’ exists

    if (!p)
        return "not found";

    switch (d_category)
    {
        case BOARD:
        case SUPERVISOR:
            return allInfo(p);
        case SALESPERSON:
            return noPhone(p);
        case CLERK:
            return nameOnly(p);
    }
}
```
```