```
class Employee : IWorkable
{
    public Employee(string name)
    {
        Name = name;
    }
    public string Name {get; set;}
    public string Work()
    {
        return "I do my job";
    }
}
abstract class Animal : IWorkable
{
    public Animal(string name)
    {
        Name = name;
    }
    public string Name {get; set;}
    public abstract string Work();
}
class Dog : Animal
{
    public Dog(string name) : base(name)
    {\}
    public override string Work()
    {
        return "I watch the house";
    }
}
class Cat : Animal
{
    public Cat(string name) : base(name)
    {\}
    public override string Work()
    {
        return "I catch mice";
    }
}
```

**Figure 10-37** The Employee, Animal, Cat, and Dog classes with the IWorkable interface

When you create a program that instantiates an Employee, a Dog, or a Cat, as in the DemoWorking program in Figure 10-38, each object type knows how to "Work()" appropriately. Figure 10-39 shows the output.