```
{ public abstract void Speak
(
    Console.WriteLine("Animals say Hello");
)
} class Lion: Animal
{
    public Lion ()
    {
    }
    public override void Speak ()
    {
        Console.WriteLine("A lion roars");
    }
}
class Bird : Animal
{
    public Bird ()
    {
    }
    public override void Speak ()
    {
        Console.WriteLine("A bird chirps.");
    }
}
```

We added a Bird class that describes the way a bird speaks, which is ultimately an overridden class that we derive from the main Animal class. This class, again, is an abstract class, so it uses the main parent class as a template for the derived child class.

# Overloading Classes

Overloading is similar to overriding, but there is a distinct difference. Overriding is done from a child class, and the method has the overriding keyword in the code. With overloading methods, you create these methods within your own classes, so it doesn't work the same as overriding. Let’s take a look at an overloaded method using the Lion class we created in the previous section.

```
abstract class Animal
{
    public abstract void Speak
(
```