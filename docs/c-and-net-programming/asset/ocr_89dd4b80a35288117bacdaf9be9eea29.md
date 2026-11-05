# For Example

```
```csharp
//a derived class method
public override void Show()
{
....
    Base.Show(); //call to base class method
....
}
```
```

# Example

```
```csharp
//illustration of runtime polymorphism
class Media
{
    public virtual void Details()
    {
        Console.writeLine("Media Details");
    }
}
class Book : Media //class Book is derived from class Media
{
    public override void Details() {
        Console.writeLine("Book Title  ERP"); }
}

Class CompactDisc:Media
{
    public override void Details() {
        Console.writeLine("Copyright is verified and License issued.");
    }
}
class Hierarchical
{
    public static void Main()
    {
        Media midi = new Media();
        midi.Details();    // own member function member function

        midi = new Book();
        midi.Details();    // derived class Book’s overridden member function
        midi = new CompactDisc();

        midi.Details();    // derived class CompactDisc’s overridden member function
    }
}
```
```