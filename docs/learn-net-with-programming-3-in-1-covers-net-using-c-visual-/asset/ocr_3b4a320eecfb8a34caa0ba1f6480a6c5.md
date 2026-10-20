# Properties

You learned from the previous chapter that private variables can only be accessed within the same class (an outside class has no access to it). However, sometimes we need to access them - and it can be done with properties.

A property is like a combination of a variable and a method, and it has two methods: a get and a set method:

Example:

```
Class Person
{

Private string name; // field

Public string Name  // property
{

Get { return name; } // get method

Set { name = value; } // set method

}
}
```