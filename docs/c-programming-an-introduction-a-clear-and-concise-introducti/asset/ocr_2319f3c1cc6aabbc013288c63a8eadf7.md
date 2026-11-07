methods can have the same name as long as there are specific differences in the parameter lists of the two methods. This is called *method overloading*. This difference has to be in the number and types of parameters in the parameter list. For example, we can have two constructor methods called Name in the Name class because one constructor has an empty parameter list (the default constructor) and the other constructor has 3 string parameters.

Using the rules of overloading, we can have the following constructor methods for the Name class (only the headings are supplied here):

```
Name();

Name(string firstName, string middleName, string lastName);

Name(string firstName, string lastName);

Name(string lastName);
```

Each of these methods has a different number of parameters in the parameter list, so when the compiler sees a call to one of them, it can differentiate it from the other method definitions.

Now let's look at a complete definition for all of these constructors:

```
Name()
{
    first = "";
    middle = "";
    last = "";
}

Name(string firstName, string middleName,
     string lastName)
{
    first = firstName;
    middle = middleName;
    last = lastName;
}
```