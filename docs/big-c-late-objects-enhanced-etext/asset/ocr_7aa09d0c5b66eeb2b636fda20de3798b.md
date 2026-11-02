To access a member of the structure, you first access the element in the array with the bracket operator, and then use the dot operator:

```
delivery_route[0].house_number = 123;
delivery_route[0].street_name = "Main Street";
```

You can also access a structure value in its entirety, like this:

```
StreetAddress start = delivery_route[0];
```

Of course, you can also form vectors of structures:

```
vector<StreetAddress> tour_destinations;
tour_destinations.push_back(white_house);
```

# 7.7.5 Structures with Array Members

Structure members can contain arrays. For example, here is a structure that describes monthly temperatures at a given location. The temperature values are stored in an array.

```
struct MonthlyTemperatures
{
    string location;
    double values[12];
};
```

To access an array element, you first select the array member with the dot notation, then use brackets:

```
MonthlyTemperatures death_valley_noon;
death_valley_noon.values[2] = 82;
```

![](bbox=[0.38, 0.6, 0.78, 0.85])

Figure 13 A Structure Containing an Array

# 7.7.6 Nested Structures

A structure can have a member that is another structure. For example, a person has a name and a street address. Because we already have a structure that describes street addresses, we can use it inside a Person structure.