```
{
    CourseId = id;
    Name = name;
}
public class Calendar
{
    public static void Schedule(int courseId)
    {
    }
    public static void Schedule(Course course)
    {
        //Something interesting happens here
    }
}
```

In this example, we have an overloaded method for Schedule — one that accepts a CourseId and one that accepts a Course reference type. The second is a reference type, because Course is a class, rather than a static type, like the Integer of the CourseId.

What if we want the second Schedule method to support an optional Course parameter? Say, if I just want it to create a New Course by default if I omit the parameter. This would be similar to setting a static integer to "0" or whatever, wouldn't it?

```
public static void Schedule(Course course = New Course())
{
    //Implementation here
}
```

This isn't allowed, however. Visual Studio allows optional parameters only on static types, and the compiler tells you so. If I want to do this, I have to accept the CourseId in the Schedule method and construct a new Course in the body of the event.

# Output parameters

As Book 1 discusses, Output parameters are parameters in the method signature that actually change the value of the variable that is passed into them by the user. The parameter references the location of the original variable, rather than creating a "working copy."

Output parameters are declared in a method signature with the out keyword. You can have as many as you like (well, within reason), although if you use more than a few, you probably should use something else (a generic list, maybe?).