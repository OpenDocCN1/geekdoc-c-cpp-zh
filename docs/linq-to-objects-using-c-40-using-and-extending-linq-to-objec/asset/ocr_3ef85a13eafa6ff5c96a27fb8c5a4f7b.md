# 208 CHAPTER 7 EXTENDING LINQ TO OBJECTS

then altered the empty source check to return default(T); rather throw new InvalidOperationException. The remaining part of the operator is unchanged (although good coding practice would have refactor out the common code into a separate method). The additional operator begins with the following:

```
public static T RandomElementOrDefault<T>(IEnumerable<T> source)
{
    // check for invalid source conditions
    if (source == null)
        throw new ArgumentNullException("source");

    if (source.Count() == 0)
        return default(T);

    //... same code as Shown in Listing 7-3 ...n}
```

Following are a few tips for developing new element operators:

+   - Remember to test and make use of any performance efficiencies offered by collections that implement IList<T> and ICollection interfaces in addition to IEnumerable<T> if present on the source collection. Make certain to support the IEnumerable<T> sequences before looking for performance optimizations.
- Implement an additional variation of these operators (suffixed with OrDefault) that returns a legal default value for a given type, rather than throw an InvalidOperationException (change the throw new InvalidOperationException to return default(T));
- Keep your extension methods in a consistent namespace so that consumers of your operators only need to add a single namespace clause to get access to your custom operators.

# Writing a Sequence Operator

The role of a sequence operator is to return IEnumerable<T> sequence based on the elements of a source sequence that have been reordered, filtered, or transformed in some way. The Where and Select standard query operators are examples of sequence operators.