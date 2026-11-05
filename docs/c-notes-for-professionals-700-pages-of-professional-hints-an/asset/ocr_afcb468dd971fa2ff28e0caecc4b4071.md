```
  " eats " + h.GetType().Name);
}
}

// <summary>
// The 'ProductA2' class
// </summary>
class Bison : Herbivore
{
}

// <summary>
// The 'ProductB2' class
// </summary>
class Wolf : Carnivore
{
    public override void Eat(Herbivore h)
    {
        // Eat Bison
        Console.WriteLine(this.GetType().Name +
            " eats " + h.GetType().Name);
    }
}

// <summary>
// The 'Client' class
// </summary>
class AnimalWorld
{
    private Herbivore _herbivore;
    private Carnivore _carnivore;

    // Constructor
    public AnimalWorld(ContinentFactory factory)
    {
        _carnivore = factory.CreateCarnivore();
        _herbivore = factory.CreateHerbivore();
    }

    public void RunFoodChain()
    {
        _carnivore.Eat(_herbivore);
    }
}
```

Output:

Lion eats Wildebeest

Wolf eats Bison

# Section 134.4: Builder Pattern

Separate the construction of a complex object from its representation so that the same construction process can create different representations and and provides a high level of control over the assembly of the objects.

In this example demonstrates the Builder pattern in which different vehicles are assembled in a step-by-step