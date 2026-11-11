The salary structure contains a member named **allowance**, which itself is a structure with three members. The members contained in the inner structure namely **dearness**, **house_rent**, and **city** can be referred to as:

```
employee.allowance.dearness
employee.allowance.house_rent
employee.allowance.city
```

An inner-most member in a nested structure can be accessed by chaining all the concerned structure variables (from outer-most to inner-most) with the member using dot operator. The following are invalid:

```
**employee.allowance** (actual member is missing)
**employee.house_rent** (inner structure variable is missing)
```

An inner structure can have more than one variable. The following form of declaration is legal:

```
struct salary
{
    .....
    struct
    {
        int dearness;
        .....
    }
    allowance,
    arrears;
}
employee[100];
```

The inner structure has two variables, **allowance** and **arrears**. This implies that both of them have the same structure template. Note the comma after the name **allowance**. A base member can be accessed as follows:

```
**employee[1].allowance.dearness**
**employee[1].arrears.dearness**
```

We can also use tag names to define inner structures. Example:

```
struct pay
{
    int dearness;
    int house_rent;
    int city;
};
struct salary
{
    char name;
    char department;
    struct pay allowance;
    struct pay arrears;
};
struct salary employee[100];
```

**pay** template is defined outside the **salary** template and is used to define the structure of **allowance** and **arrears** inside the **salary** structure.

It is also permissible to nest more than one type of structures.