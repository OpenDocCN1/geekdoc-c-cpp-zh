```
get { return color; }
set { color = value; }
```

The get method must be used for returning the variable. On the other hand, the set method must be used for assigning a value to that variable. Of course, the above example is a very simple example of a code involving a property. As such, it is certainly possible to extend it further.

There is another thing that you should understand about properties. A property requires at least one method to work. In other words, you can use either a get method or a set method. The other method becomes optional in these cases. This technique allows you to define read-only properties or write-only properties as per your requirements.

Here is another example that further illustrates the potential of properties.

```
public string Color
{
get
{
return color.ToUpper();
}
}
```