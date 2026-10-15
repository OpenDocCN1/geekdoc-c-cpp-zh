```
public class MyClass
{
    public int a;
    public string b;

    public void MyMethod()
    {
        Console.WriteLine("Hello world");
    }
}
```

First, we have the class definition using the class keyword followed by the name of the class. Here, that would be MyClass. I've prefixed MyClass with an access modifier, here public, making the class accessible from pretty much everywhere. Then, again, between a pair of curly braces, I have the class body. In there, we will have the code for our class. They also creates the scope. When creating a field, a or b, here inside of the class, that field is available in the body of the class. Inside of the body of a class, we can write our code. We can use fields. I have introduced fields in the last chapter. They are basically variables that will hold the data. We'll also include methods, which will contain the functionality and work on the class data. Later in this chapter, we'll learn that our data is typically accessible through properties, which will wrap the field data, but more on that later. Also, classes can contain events. Events are used to enable classes to notify other classes about something interesting that happened, such as a button click. I'm sure you now already understand what classes are about. Let's start going practical now and create one. I'm going to take you through the steps of creating