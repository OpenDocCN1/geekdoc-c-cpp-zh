```
Contract.Requires(CalculatedCutFactor(factorModifier) >= 0);
    return volumeSteel / (CutFactor * factorModifier);
}

/// <summary>
/// This is a pure method
/// </summary>
/// <param name="factorModifier"></param>
/// <returns></returns>
[Pure]
public int CalculatedCutFactor(int factorModifier)
{
    return CutFactor * factorModifier;
}
}
```

Code Listing 58: Pure Method Marked as Pure

The CalculatedCutFactor method is now a pure method because it does not change the values of CutFactor or factorModifier. It can now suitably be decorated with the [Pure] attribute. Our Contract.Requires in the VolumeCut method can now use this pure method to check that the result of CalculatedCutFactor will not be zero, because this would result in a divide by zero exception on the return.

Method purity is a really good practice to follow, not only when using Code Contracts, but in every method you write.

# Contract abbreviator methods

I am sure that those of you who use Code Contracts on a regular basis have run into the issue of repeating similar sets of Code Contracts across multiple methods. Code Contracts have a solution for this, and they are called abbreviator methods. The concept is really simple. You can see that the code in Code Listing 59 contains repeated sets of Code Contracts.

```
public class AbbreviatorDemo
{
    /// <summary>
    /// The factor for the cutting volume
    /// </summary>
    public int Factor { get; private set; }
    /// <summary>
    /// The maximum volume a bin can contain
    /// </summary>
    public int MaxVolume { get; private set; }

    /// <summary>
```