Click here to view code image

```
office make_office(float floor_space, int staff,
bool two_floors = false);
```

One speedy recompilation later and all remains right with the world.
Unfortunately, the demons of domain expansion are not finished with you yet: it turns out that the single-floor offices sometimes need the name of the building they will be situated in. You, the ever-accommodating engineer, expand your function's parameter list once again:

Click here to view code image

```
office make_office(float floor_space, int
staff,bool two_floors = false,
    std::string const& building_name = {});
```

You reimplement your function, but it irritates you. There are four arguments, the final argument will only be needed if the third argument is false, and it all looks messy and complicated. You decide to overload your function:

Click here to view code image

```
office make_office(float floor_space, int staff,
bool two_floors = false);
office make_office(float floor_space, int staff,
    std::string const& building_name);
```

You now have what is known as a function overload set, and it is up to the compiler to choose which member of the set to invoke according to the arguments passed in. The client is forced to call the correct function when a building must be identified. Identification implies a single-floor office.
For example, some client code may wish to create an office with 24,000 square meters of space for 200 people. The office is situated on one floor in a building called “Eagle Heights.” The correct invocation is therefore

Click here to view code image