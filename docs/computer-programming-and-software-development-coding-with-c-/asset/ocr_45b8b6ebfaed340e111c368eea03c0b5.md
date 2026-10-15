```
{
    public class Organization
    {
        public int Id { get; set; }
        public string? Name { get; set; }

        public override string ToString() => $"Id: {Id}, Name: {Name}";
    }
}
```

So you see here just the methods of the object type. But what I want to do here is to grab the Id property and to compare it with the Id that comes in as a parameter into that method. But as you can see, I cannot access here this Id property. I have only the members of the object type. Now let's change this. Let's go to the Solution Explorer, and let's open here the Employee C# file. As you can see, this class has an Id property, and when I open the Organization class, you can see it has also an Id property. This means you can create a base class that contains that Id property. So let me cut the Id property from here, and let's create directly in this file a new class that I call EntityBase, and in that class, I specify the Id property. Now let's inherit the Organization class from EntityBase so it has again the Id property that comes now from the base class.