To support the introduction of generics, the BCL team added various generic collection types to the System.Collections.Generic namespace, an example of which is illustrated in the code fragment here:

```
    List<int> primes = new List<int>();
    for (int n = 2; n <= 100; n++)
    {
        bool isPrime = true;
        for (int d = 2; d <= Math.Sqrt(n); d++)
        {
            if (n % d == 0)
            {
                isPrime = false;
                break;
            }
        }

        if (isPrime)
            primes.Add(n); // statically typed to take in an integer value
    };

    // no performance hit to convert types when retrieving data
    foreach (int prime in primes)
        Console.WriteLine(prime);
```

Generics offer better static typing, thus doing away with whole classes of code defects and various performance benefits because they eliminate the need for runtime type conversions.

# ## Nullable Types

During the design of the first release of the CLI, a distinction had been made between value types and reference types. Value types are stack allocated, whereas reference types live on the managed heap. Therefore, reference types can have null values (conceptually comparable to null pointers in native languages), whereas value types cannot.

The lack of an orthogonal approach in the classification of types versus their nullability was seen as an oversight that was rectified in the second release of .NET Framework with the introduction of nullable value types. This proves especially handy when mapping database records to objects because nullability applies to all types in the world of (relational) databases.

The following is an example of the use of nullable types, denoted with a ? suffix:

```
    int a = null; // won't compile; int is a value type and cannot be set to null
    int? b = null; // valid in C# 2.0 and above
```