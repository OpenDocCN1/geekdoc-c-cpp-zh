```
}
else
{
    Console.WriteLine(
        @"Collection ""SequenceEquals""" +
        $"{{{nameof(numbers)}}.Concat(odd).Distinct()}}")
}
Print("Reverse: {0}", numbers.Reverse());
Print("Average: {0}", numbers.Average());
Print("Sum: {0}", numbers.Sum());
Print("Max: {0}", numbers.Max());
Print("Min: {0}", numbers.Min());
}

private static void Print<T>(
    string format, IEnumerable<T> items) =>
    Console.WriteLine(format, string.Join(
        ", ", items.Select(x => x.ToString())));

private static void Print<T>(string format, T item)
{
    Console.WriteLine(format, item);
}
}
```

# OUTPUT 14.13

```
Stuff: System.Object, 1, 3, 5, 7, 9, "thing"
24c24a41-ee05-4b9-958e-50dd12e3981e
Even integers: 0, 2, 4, 6, 8
Odd integers: 1, 3, 5, 7, 9
Union of odd and even: 0, 2, 4, 6, 8, 1, 3, 5, 7, 9
Union with even: 0, 2, 4, 6, 8, 1, 3, 5, 7, 9
Concat with odd: 0, 2, 4, 6, 8, 1, 3, 5, 7, 9, 1, 3, 5, 7, 9
Intersection with even: 0, 2, 4, 6, 8
Distinct: 0, 2, 4, 6, 8, 1, 3, 5, 7, 9
Collection "SequenceEquals" numbers.Concat(odd).Distinct()
Reverse: 9, 7, 5, 3, 1, 8, 6, 4, 2, 0
Average: 4.5
Sum: 45
Max: 9
Min: 0
```

None of the API calls in Listing 14.21 requires a lambda expression. Table 14.1 and Table 14.2 describe each method and provide an example. Included on System.Linq.Enumerable is a collection of aggregate functions that enumerate the collection and calculate a result (shown In Table 14.2). Count is one example of an aggregate function already shown within the chapter.