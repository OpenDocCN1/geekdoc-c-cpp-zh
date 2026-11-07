```
```text
Name(string firstName, string lastName)
{
    first = firstName;
    middle = "";
    last = lastName;
}
```
```

```
```text
Name(string lastName)
{
    first = "";
    middle = "";
    last = lastName;
}
```
```

The Name constructor with two parameters will create an object with a first and last name and just the empty string for the middle name, while the last constructor will create an object with empty string for the first and middle names and the passed-in value for the last name. Of course, the last constructor was just picked because it is just assumed that a Name object would not be created with just a first or a middle name and not a last name.

# *Class Get and Set Methods*

Once an object has been created, and data stored in the members, you need ways to get data into and out of the object. A well-designed class provides a group of methods that return member values from the object and assign values to the members. These are called get and set methods.

Let’s start with set methods. We looked at one example of a set method earlier, the setName() method. This method sets the values of all the members in one method call. We also need set methods for each individual member. Here are the set methods we need for the Name class: