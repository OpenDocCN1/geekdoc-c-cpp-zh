possibly their default implementations). We will come back to interfaces in the next part.

# .NET Types

# Tuples

C# provides a very convenient syntax for values and variables of the System.ValueTuple type. The tuples can be used, for example, to return multiple values from a method (syntactically). We also used deconstructions in a number of examples.

# DateTime and TimeSpan

DateTime and TimeSpan are a few of the most commonly used types in C# programs.

# System.Random

We used an instance of the System.Random class to fetch random numbers (integers of floating point numbers). A Random variable needs to be "seeded", and it generates a sequence of "pseudorandom numbers".

# .NET Collection Types

We used a couple of .NET collection types, including List<T> and Dictionary<K, V>. These are reference types just like arrays.

A list stores a list of items (objects), an a dictionary stores key-value pairs.

# Yield Return

We introduced a special syntax in C# to create a method that returns an IEnumerable<T>, using the yield return statement.