```
if (copy is null)
{
    copy = c; // copy and c refer to the same object
    ...
}
```

> Note You can also use == null to check for a null reference. However, is null reads more naturally. Similarly, you can use is not null as well as != null to check for a non-null reference.

# The null-conditional and null-coalescing operators

The null-conditional operator enables you to test for null values succinctly. To use the null-conditional operator, append a question mark (?) to the name of your variable.

For example, suppose you attempt to call the Area method on a Circle object when the Circle object has a null value:

Click here to view code image

```
Circle c = null;
Console.WriteLine($"The area of circle c is {c.Area()}");
```

In this case, the Circle.Area method throws a NullReferenceException, which makes sense because you cannot calculate the area of a circle that does not exist.

To avoid this exception, you could test whether the Circle object is null before you attempt to call the Circle.Area method:

Click here to view code image

```
if (c is not null)
{
    Console.WriteLine($"The area of circle c is {c.Area()}");
}
```