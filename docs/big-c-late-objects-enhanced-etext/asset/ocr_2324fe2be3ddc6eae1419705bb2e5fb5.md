```
struct Person
{
    string name;
    StreetAddress work_address;
};
```

You can access the nested member in its entirety, like this:

```
Person theodore;
theodore.work_address = white_house;
```

Alternatively, if you want to select a member of a member, use the dot operator twice:

```
theodore.work_address.street_name = "Pennsylvania Avenue";
```

A structure can have multiple members that are structures. For example, Person can also have a home address that again has type StreetAddress:

```
struct Person
{
    string name;
    StreetAddress home_address;
    StreetAddress work_address;
};
```

![](bbox=[0.35, 0.6, 0.78, 0.78])

Figure 14 A Structure Containing Another Structure

EXAMPLE CODE See sec07 of your companion code for a program that shows structures in use.

# 7.8 Pointers and Structures

# 7.8.1 Pointers to Structures

It is common to allocate structure values dynamically. As with all dynamic allocations, you use the new operator:

```
StreetAddress* address_pointer = new StreetAddress;
```

Now suppose you want to set the house number of the structure to which address_pointer points. As always when you have a pointer, you can use the * operator for