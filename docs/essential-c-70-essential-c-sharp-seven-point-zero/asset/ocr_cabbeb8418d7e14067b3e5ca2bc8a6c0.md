```
```csharp
private static void Print<T>(IEnumerable<T> items)
{
    foreach (T item in items)
    {
        Console.WriteLine(item);
    }
}
```
```

```
```csharp
public static class PatentData
{
    public static readonly Inventor[] Inventors = new Inventor[]
    {
        new Inventor(){
            Name="Benjamin Franklin", City="Philadelphia",
            State="PA", Country="USA", Id=1 },
        new Inventor(){
            Name="Orville Wright", City="Kitty Hawk",
            State="NC", Country="USA", Id=2},
        new Inventor(){
            Name="Wilbur Wright", City="Kitty Hawk",
            State="NC", Country="USA", Id=3},
        new Inventor(){
            Name="Samuel Morse", City="New York",
            State="NY", Country="USA", Id=4},
        new Inventor(){
            Name="George Stephenson", City="Wylam",
            State="Northumberland", Country="UK", Id=5},
        new Inventor(){
            Name="John Michaelis", City="Chicago",
            State="IL", Country="USA", Id=6},
        new Inventor(){
            Name="Mary Phelps Jacob", City="New York",
            State="NY", Country="USA", Id=7},
    };
```
```

```
```csharp
public static readonly Patent[] Patents = new Patent[]
{
    new Patent(){
        Title="Bifocals", YearOfPublication="1784",
        InventorIds=new long[] {1}},
    new Patent(){
        Title="Phonograph", YearOfPublication="1877",
        InventorIds=new long[] {1}},
    new Patent(){
        Title="Kinetoscope", YearOfPublication="1888",
        InventorIds=new long[] {1}},
    new Patent(){
        Title="Electrical Telegraph",
        YearOfPublication="1837",
        InventorIds=new long[] {4},
```
```