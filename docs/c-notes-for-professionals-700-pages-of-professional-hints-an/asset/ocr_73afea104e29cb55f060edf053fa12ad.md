```
public class Cat : Animal
{
    public Cat()
    {
        Name = "Cat";
    }
    // Methods for scratching furniture and ignoring owner
    public void Scratch(Object furniture)
    {
        // ...
    }
}
```

The Cat class gets access to not only the methods described in its definition explicitly, but also all the methods defined in the general Animal base class. Any Animal (whether or not it was a Cat) could Eat, Stare, or Roll. An Animal would not be able to Scratch, however, unless it was also a Cat. You could then define other classes describing other animals. (Such as Gopher with a method for destroying flower gardens and Sloth with no extra methods at all.)

# Section 58.3: Inheriting from a class and implementing an interface

```
public class Animal
{
    public string Name { get; set; }
}

public interface INoiseMaker
{
    string MakeNoise();
}

//Note that in C#, the base class name must come before the interface names
public class Cat : Animal, INoiseMaker
{
    public Cat()
    {
        Name = "Cat";
    }

    public string MakeNoise()
    {
        return "Nyan";
    }
}
```

# Section 58.4: Inheriting from a class and implementing multiple interfaces

```
public class LivingBeing
{
    string Name { get; set; }
}

public interface IAnimal
{
    bool HasHair { get; set; }
}
```