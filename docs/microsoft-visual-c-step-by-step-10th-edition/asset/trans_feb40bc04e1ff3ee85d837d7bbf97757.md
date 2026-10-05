

```csharp
static class Utils
{
    public static int ConvertToBase(this int i, int baseToConvertTo)
    {
    }
}
```

```csharp
public static int ConvertToBase(this int i, int baseToConvertTo)
{
    if (baseToConvertTo < 2 || baseToConvertTo > 10)
    {
        throw new ArgumentException("Value cannot be converted to base " + baseToConvertTo.ToString());
    }
}
```

```csharp
public static int ConvertToBase(this int i, int baseToConvertTo)
{
    ... 
    int result = 0;
    int iterations = 0;
    do
    {
        int nextDigit = i % baseToConvertTo;
        i /= baseToConvertTo;
        result += nextDigit * (int)Math.Pow(10, iterations);
        iterations++;
    } while (i != 0);
    return result;
}
```

```csharp
static void doWork()
{
    int x = 591;
    for (int i = 2; i <= 10; i++)
    {
        Console.WriteLine($"{x} in base {i} is {x.ConvertToBase(i)}");
    }
}
```

```csharp
class DerivedClass : BaseClass {
  ...
}
```

```csharp
class DerivedClass : BaseClass
{
    ...
    public DerivedClass(int x) : base(x)
    {
        ...
    }
    ...
}
```

```csharp
class Mammal
{
    public virtual void Breathe()
    {
        ...
    }
    ...
}
```

```csharp
class Whale : Mammal
{
    public override void Breathe()
    {
        ...
    }
    ...
}
```

```csharp
static class Utils
{
    public static int Negate(this int i)
    {
        return -i;
    }
}
```

```csharp
int CompareTo(object obj)
{
    // return 0 if this instance is equal to obj
    // return < 0 if this instance is less than obj
    // return > 0 if this instance is greater than obj
    ...
}
```

```csharp
interface IComparable
{
    int CompareTo(object obj);
}
```

```csharp
class Horse : ILandBound
{
    ...
    public int NumberOfLegs()
    {
        return 4;
    }
}
```

```csharp
interface ILandBound
{
  ...
}
```

```csharp
class Mammal
{
  ...
}
```

```csharp
class Horse : Mammal , ILandBound
{
  ...
}
```

```csharp
Horse myHorse = new Horse(...);
ILandBound iMyHorse = myHorse; // legal
```

```csharp
int FindLandSpeed(ILandBound landBoundMammal)
{
    ...
}
```

```csharp
if (myHorse is ILandBound)
{
    ILandBound iLandBoundAnimal = myHorse;
}
```

```csharp
class Horse : Mammal, ILandBound, IGrazable
{
    ...
}
```

```csharp
interface ILandBound
{
    int NumberOfLegs();
}

class Horse : ILandBound
{
    ...
    public int NumberOfLegs()
    {
        return 4;
    }
}
```

```csharp
class Horse : ILandBound, IJourney
{
    ...
    public int NumberOfLegs()
    {
        return 4;
    }
}
```

```csharp
class Horse : ILandBound, IJourney
{
    ...
    int ILandBound.NumberOfLegs()
    {
        return 4;
    }

    int IJourney.NumberOfLegs()
    {
        return 3;
    }
}
```

```csharp
Horse horse = new Horse();
...
// The following statement will not compile
int legs = horse.NumberOfLegs();
```

```csharp
Horse horse = new Horse();
...
Journey journeyHorse = horse;
int legsInJourney = journeyHorse.NumberOfLegs();
ILandBound landBoundHorse = horse;
int legsOnHorse = landBoundHorse.NumberOfLegs();
```

```csharp
public interface IMyInterface
{
    public void DoSomeWork();
}
```

```csharp
public class myClass : IMyInterface
{
    void IMyInterface.DoSomeWork()
    {
        // Implementation
        ...
    }
}
```

```csharp
public interface IMyInterface
{
    public void DoSomeWork();
    public void DoAdditionalWork();
}
```

```csharp
public interface IMyExtendedInterface : IMyInterface
{
    public void DoAdditionalWork();
}
```

```csharp
public interface IMyInterface
{
    public void DoSomeWork();
    public void DoAdditionalWork()
    {
        throw new NotImplementedException();
    }
}
```

```csharp
public class myNewClass : IMyInterface
{
    void IMyInterface.DoSomeWork()
    {
        // Implementation
        ...
    }

    void IMyInterface.DoAdditionalWork()
    {
        // Implementation
        ...
    }
}
```

