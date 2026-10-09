# Enabling Covariance with the out Type Parameter Modifier in C# 4.0 (and Later)

You might have noticed that both problems described earlier as consequences of unrestricted covariance arise because the generic pair and the generic list allow their contents to be written. Suppose we eliminated this possibility by making a read-only IReadOnlyPair<T> interface that exposes T only as coming “out” of the interface (i.e., used as the return type of a method or read-only property) and never going “into” it (i.e., used as a formal parameter or writeable property type). If we restricted ourselves to an “out only” interface with respect to T, the covariance problem just described would not occur (see Listing 12.42).

# LISTING 12.42: Potentially Possible Covariance

```
```
interface IReadOnlyPair<T>
{
  T First { get; }
  T Second { get; }
}

interface IPair<T>
{
  T First { get; set; }
  T Second { get; set; }
}

public struct Pair<T> : IPair<T>, IReadOnlyPair<T>
{
  // ...
}

class Program
{
  static void Main()
  {
    // Error: Only theoretically possible without
    // the out type parameter modifier
    Pair<Contact> contacts =
      new Pair<Contact>(
        new Contact("Princess Buttercup"),
        new Contact("Inigo Montoya") );
    IReadOnlyPair<PdaItem> pair = contacts;
    PdaItem pdaItem1 = pair.First;
    PdaItem pdaItem2 = pair.Second;
  }
}
```
```