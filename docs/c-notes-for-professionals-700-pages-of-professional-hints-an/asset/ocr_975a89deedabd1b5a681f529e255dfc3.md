On a surface level, the CompareTo method in our item simply returns the difference in their ID numbers, but what does the above do in practice?

Now, when we call Sort() on a List<Item> object, the List will automatically call the Item's CompareTo method when it needs to determine what order to put objects in. Furthermore, besides List<T>, any other objects that need the ability to compare two objects will work with the Item because we have defined the ability for two different Items to be compared with one another.

# Section 41.5: Implementing multiple interfaces

```
```csharp
public interface IAnimal
{
    string Name { get; set; }
}

public interface INoiseMaker
{
    string MakeNoise();
}

public class Cat : IAnimal, INoiseMaker
{
    public Cat()
    {
        Name = "Cat";
    }

    public string Name { get; set; }

    public string MakeNoise()
    {
        return "Nyan";
    }
}
```
```

# Section 41.6: Why we use interfaces

An interface is a definition of a contract between the user of the interface and the class that implement it. One way to think of an interface is as a declaration that an object can perform certain functions.

Let's say that we define an interface IShape to represent different type of shapes, we expect a shape to have an area, so we will define a method to force the interface implementations to return their area :

```
```csharp
public interface IShape
{
    double ComputeArea();
}
```
```

Let's that we have the following two shapes : a Rectangle and a Circle

```
```csharp
public class Rectangle : IShape
{
    private double length;
    private double width;

    public Rectangle(double length, double width)
    {
        this.length = length;

```