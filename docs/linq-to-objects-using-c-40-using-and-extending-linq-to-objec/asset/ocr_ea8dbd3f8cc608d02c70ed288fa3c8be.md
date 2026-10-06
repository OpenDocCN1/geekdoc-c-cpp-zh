operators implement a variant of these operators that return a null value or a default value you specify. The operators FirstOrDefault and LastOrDefault are examples that carry out the basic function of their parts, but instead of throwing an exception when the source sequence is empty, they return the default value of the type by calling the default keyword on the specific underlying generic type. For our Last implementation, we would add an operator called LastOrDefault, and the code for the final operator would be (the only alteration from the code for the final operator is the operator's name and the last line):

```
public static T LastOrDefault<T>(
    // ... Same code as shown in Listing 7-2 except ...
    // throw new InvalidOperationException("No elements");
    //
    // BECOMES -

    return default(T);

```

# WHAT DOES THE DEFAULT KEYWORD RETURN?

The default keyword solves the issue of not knowing what default value to initially assign to a generic type and returns null for reference types and zero for numeric value types. For structs, it will return each member of the struct initialized to zero or null, depending on whether they are value or reference types.

# Building the RandomElement Operator

To demonstrate how to build a custom operator that returns a single element from a source sequence, let's look at an operator that returns an element at random. There are often times when picking a candidate at random from a collection is necessary, either for test data or deriving a random sample from a customer list to provide specific advertising or business offers. This new operator will be called RandomElement and will return one element at random from a given sequence (pseudo-random to be exact—it can be difficult to get the randomness you need for a small collection or when retrieving more than one in a tight loop).