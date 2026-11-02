# Syntax 7.3 Defining a Structure

![](bbox=[0.28, 0.15, 0.9, 0.6])

This definition yields a new type, StreetAddress, that you can use for declaring variables:

```
StreetAddress white_house;
```

The variable white_house has two named parts, called members, house_number and street_name. You use the "dot notation" to access each member, like this:

```
white_house.house_number = 1600;
white_house.street_name = "Pennsylvania Avenue";
```

> You use the dot notation to access members of a structure.

![](bbox=[0.48, 0.7, 0.73, 0.8])

Figure 11 A Structure Value

# 7.7.2 Structure Assignment and Comparison

> When you assign one structure value to another, all members are assigned.

You can use the = operator to assign one structure value to another. All members are assigned simultaneously. For example, if we declare a structure value

```
StreetAddress destination;
```

then the assignment

```
destination = white_house;
```

is equivalent to

```
destination.house_number = white_house.house_number;
destination.street_name = white_house.street_name;
```