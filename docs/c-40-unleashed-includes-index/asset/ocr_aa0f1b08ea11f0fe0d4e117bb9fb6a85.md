# The foreach Statement

One of the most common sources of loop constructs enumerating over a collection of some sort and executing some code for all the elements found. Welcome the foreach statement, which provides you with this functionality.

Before we delve into details, let's take a look at a few examples. The simplest collection type is the array. Instead of writing a for loop that goes over a range of indices using the array's Length property as an exclusive upper bound, we can write the following:

```
int[] primes = new int[] { 2, 3, 5, 7 };
foreach (int prime in primes)
{
    Console.WriteLine(prime);
}
```

The foreach statement breaks down into the following pieces:

```
foreach (type identifier in expression)
    embedded-statement
```

Here, expression represents the source of the loop. You'll see in just a minute what expressions can be used for enumeration. In front of the in keyword, a local variable—referred to as the iteration variable—is introduced. For every iteration, it will take on the value of an element found in the source.

Another example can be found with the collection types. I'm using the generic ones from the System.Collections.Generic namespace here:

```
var primes = new List<int> { 2, 3, 5, 7 };
foreach (int prime in primes)
{
    Console.WriteLine(prime);
}

var ages = new Dictionary<string, int> { { "Bart", 26 }, { "John", 62 } };
foreach (string name in ages.Keys)
{
    Console.WriteLine("{0} is {1}", name, ages[name]);
}
```

The first example should be self-explanatory. In the last one, we're using the Keys property of the Dictionary<K,T> generic type to get all the keys back that appear in the dictionary. Inside the loop, we index into the collection based on that key to retrieve the age. This is just one technique: