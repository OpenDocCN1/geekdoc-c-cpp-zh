by making the initialization independent of the field order:

```
struct employee emp = {.name="alice_smith",.employee_no=1200,.salary=10000};
```

# Passing Structs to Functions

A struct can be passed to a function by value or by reference (pointer).

# Arrow Operator

Suppose that we have a pointer to a struct:

```
struct employee emp = {"alice_smith", 123, 10000};
struct employee* ptrEmployee;
```

```
ptrEmployee = &emp;
```

We can address members of emp as follows:

```
ptrEmployee->name;
```

This is the same as:

```
(*ptrEmployee).name;
```