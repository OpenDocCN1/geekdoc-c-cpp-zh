```
Console.WriteLine();

// Compute the area per person in office.
areaPP = office.Area / office.Occupants;

Console.WriteLine("office has:\n " +
    office.Floors + " floors\n " +
    office.Occupants + " occupants\n " +
    office.Area + " total area\n " +
    areaPP + " area per person");
}
```

The output produced by this program is shown here:

house has:
  2 floors
  4 occupants
  2500 total area
  625 area per person

office has:
  3 floors
  25 occupants
  4200 total area
  168 area per person

As you can see, house's data is completely separate from the data contained in office. Figure 6-1 depicts this situation.

# How Objects Are Created

In the preceding programs, the following line was used to declare an object of type Building:

```
Building house = new Building();
```

This declaration performs three functions. First, it declares a variable called house of the class type Building. This variable is not, itself, an object. Instead, it is simply a variable that can refer to an object. Second, the declaration creates an actual, physical copy of the object.

FIGURE 6-1
One object's instance variables are separate from another's.

![](bbox=[0.35, 0.88, 0.85, 0.98])