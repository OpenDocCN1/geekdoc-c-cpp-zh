# ADVANCED TOPIC

# Customizing Dictionary Equality

To determine whether a given key matches any existing key in the dictionary, the dictionary must be able to compare two keys for equality. This is analogous to the way that lists must be able to compare two items to determine their order. (For an example, see the Advanced Topic, “Customizing Collection Sorting,” earlier in this chapter.) By default, two instances of a value type are compared by checking whether they contain exactly the same data, and two instances of a reference type are compared to see whether both reference the same object. However, it is occasionally necessary to be able to compare two instances as equal even if they are not exactly the same value or exactly the same reference.

For example, suppose you wish to create a Dictionary<Contact, string> using the Contact type from Listing 16.2. However, you want any two Contact objects to compare as equal if they have the same first and last names, regardless of whether the two objects are reference equal. Much as you can provide an implementation of IComparer<T> to sort a list, so you can similarly provide an implementation of IEqualityComparer<T> to determine if two keys are to be considered equal. This interface requires two methods: one that returns whether two items are equal, and one that returns a “hash code” that the dictionary can use to facilitate fast indexing. Listing 16.8 shows an example.

# LISTING 16.8: Implementing IEqualityComparer<T>

```
using System;
using System.Collections.Generic;

class ContactEquality : IEqualityComparer<Contact>
{
    public bool Equals(Contact x, Contact y)
    {
        if (Object.ReferenceEquals(x, y))
            return true;
        if (x == null || y == null)
            return false;
        return x.LastName == y.LastName &&
            x.FirstName == y.FirstName;
    }

    public int GetHashCode(Contact x)
    {
```