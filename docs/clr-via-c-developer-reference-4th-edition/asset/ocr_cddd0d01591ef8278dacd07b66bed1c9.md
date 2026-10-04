# Thread Stack

# Heap

| Manager Object | Manager Type Object |
| :--- | :--- |
| Type object ptr | Type object ptr |
| Sync block index | Sync block index |
| Instance fields | Static fields |
| | GetProgressReport |

| e (Employee) | = 0 |
| :--- | :--- |
| year (int32) | |

| Employee Type Object |
| :--- |
| Type object ptr |
| Sync block index |
| Static fields |
| GetYearsEmployed |
| GetProgressReport |

```
void M3() {
  Employee e;
  Int32 year;
  e = new Manager();
  e = Employee.Lookup("joe");
  year = e.GetYearsEmployed();
  e.GetProgressReport();
}
```

FIGURE 4-9 Allocating and initializing a Manager object.

# Thread Stack

# Heap

| Manager Object | Manager Type Object |
| :--- | :--- |
| Type object ptr | Type object ptr |
| Sync block index | Sync block index |
| Instance fields | Static fields |
| | GetProgressReport |

| e (Employee) | = 0 |
| :--- | :--- |
| year (int32) | |

| Manager Object |
| :--- |
| Type object ptr |
| Sync block index |
| Instance fields |

| Employee Type Object |
| :--- |
| Type object ptr |
| Sync block index |
| Static fields |
| GetYearsEmployed |
| GetProgressReport |

```
void M3() {
  Employee e;
  Int32 year;
  e = new Manager();
  e = Employee.Lookup("joe");
  year = e.GetYearsEmployed();
  e.GetProgressReport();
}
```

![](bbox=[0.775, 0.715, 0.82, 0.765])

FIGURE 4-10 Employee's static Lookup method allocates and initializes a Manager object for Joe.

CHAPTER 4 Type Fundamentals 107