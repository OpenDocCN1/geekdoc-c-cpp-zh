```
// various members
}
```

At some point in the future, you write a derived class Ellipse that adds some functionality to the Shape base class. In particular, you add a method called MoveBy, which is not present in the base class:

```
public class Ellipse: Shape
{
    public void MoveBy(int x, int y)
    {
        Position.X += x;
        Position.Y += y;
    }
}
```

At some later time, the developer of the base class decides to extend the functionality of the base class and, by coincidence, adds a method that is also called MoveBy and that has the same name and signature as yours; however, it probably doesn’t do the same thing. This new method might be declared virtual or not.

If you recompile the derived class you get a compiler warning because of a potential method clash. However, it can also happen easily that the new base class is used without compiling the derived class; it just replaces the base class assembly. The base class assembly could be installed in the global assembly cache (which is done by many Framework assemblies).

Now let’s assume the MoveBy method of the base class is declared virtual and the base class itself invokes the MoveBy method. What method will be called? The method of the base class or the MoveBy method of the derived class that was defined earlier? Because the MoveBy method of the derived class is not defined with the override keyword (this was not possible because the base class MoveBy method didn’t exist earlier), the compiler assumes the MoveBy method from the derived class is a completely different method that doesn’t have any relation to the method of the base class; it just has the same name. This method is treated the same way as if it had a different name.

Compiling the Ellipse class generates a compilation warning that reminds you to use the new keyword to hide a method. In practice, not using the new keyword has the same compilation result, but you avoid the compiler warning:

```
public class Ellipse: Shape
{
    new public void Move(Position newPosition)
    {
        Position.X = newPosition.X;
        Position.Y = newPosition.Y;
    }
    //... other members
}
```

Instead of using the new keyword, you can also rename the method or