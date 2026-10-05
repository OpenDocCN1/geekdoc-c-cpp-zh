# 1.3. C++ review

| 2 | 1 | |
| v.size | v.data | v.owner v(0) | v(1) |

Figure 1.5: Schematic picture of a Vector of length 2, which “owns” its data.

The listing shows the outline of the definition of the class Vector (lines 12 through 17). There is a private section (line 13) in the class definition and a public section (line 15). The class definition must end with a semicolon as on line 17. Omitting the semicolon at the end of class definitions is a common novice error.

# Private section of the Vector class

A class is a collection of data members and member functions. In the Vector class all the data members are in the private section.

```
class Vector{
private:
    long int size;
    double *data;
    int owner;
    ...
};
```

The class member size is the length of the vector and data is a pointer to the contents of the vector; so data[i] is in effect a name for the ith entry of the vector. The owner field will be either 0 or 1—meaning is explained later.

If v is a variable of type Vector, then it is a name for a segment of memory that includes a location of type int, a location of type double *, and a location of type int. A schematic view of a Vector of length 2 is shown in figure 1.5. If v is the name