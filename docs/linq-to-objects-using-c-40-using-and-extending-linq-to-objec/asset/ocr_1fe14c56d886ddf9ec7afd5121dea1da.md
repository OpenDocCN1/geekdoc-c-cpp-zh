# 202 CHAPTER 7 EXTENDING LINQ TO OBJECTS

The RandomElement operator has the following requirements:

+   * Take an input source IEnumerable<T> sequence and return one element at random.
* Allow control over the random number generator by optionally accepting a seed value.
* Throw an ArgumentNullException if the source sequence is null.
* Throw an InvalidOperationException if the source sequence is empty.

As seen when implementing the Last operator, although it is certain that sequences you extend the IEnumerable<T> interface, any sequences also implement the IList<T> and ICollection<T> interfaces, which can be used to improve performance. Any collection type that implements IList allows elements to be accessed by index position (for example, list[2] will return the third element), and any collection implementing ICollection exposes a Count property that immediately retrieves element count. These performance enhancements should be used if possible.

The code shown in Listing 7-3 uses the built-in .NET Framework random number generator to find an index position within a sequence's bounds and returns that element. It first tries to retrieve the element (because it is faster), and if that interface isn't supported by the collection, this operator uses a slower enumeration looping pattern (completely valid code, just slower).

# OPTIONAL PARAMETERS IN C# 4.0 Listing 7-3 demonstrates the use of optional parameters in the method declaration. This is covered in Chapter 8, "C# 4.0 Features," in detail but here to demonstrate that the value for seed is optional. If this method is called by omitting a value for seed, its value is 0 in the method.

# Listing 7-3 Sample RandomElement operator returns an element at random from a source sequence and takes an optional seed value for the random number generator

```
public static T RandomElement<T>(
    IEnumerable<T> source,
    int seed = 0 / /* optional param, new to C# 4.0(see Chapter 8) */)
{
    // check for null source conditions
    if (source == null)
        throw new ArgumentNullException("source");
```