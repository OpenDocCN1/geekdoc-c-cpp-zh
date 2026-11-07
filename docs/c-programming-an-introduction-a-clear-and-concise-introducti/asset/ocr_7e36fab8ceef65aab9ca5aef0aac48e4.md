```
void setFirst(string firstName)
{
    first = firstName;
}

void setMiddle(string middleName)
{
    middle = middleName;
}

void setLast(string lastName)
{
    last = lastName;
}
```

Now, if a Name object has a name change that doesn't involve the whole name, we can call whichever of the set methods we need. For example:

```
Name myName("Mary", "Alice", "Smith");
cout << myName.displayName() << endl;
// Mary gets married to Joe Brown
myName.setLast("Brown");
cout << myName.displayName() <<endl;
```

The output is:

```
Mary Alice Smith
Mary Alice Brown
```

We also need methods that return the information individually, and not just as a group, as getName() does. Get methods provide this capability. Here are the get methods for the Name class: