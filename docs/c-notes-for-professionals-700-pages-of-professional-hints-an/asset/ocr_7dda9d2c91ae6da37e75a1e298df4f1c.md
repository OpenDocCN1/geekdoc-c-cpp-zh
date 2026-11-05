# Section 149.4: Create multiple random class with different seeds simultaneously

Two Random class created at the same time will have the same seed value.

Using System.Guid.NewGuid().GetHashCode() can get a different seed even in the same time.

```
Random rnd1 = new Random();
Random rnd2 = new Random();
Console.WriteLine("First 5 random number in rnd1");
for (int i = 0; i < 5; i++)
    Console.WriteLine(rnd1.Next());
Console.WriteLine("First 5 random number in rnd2");
for (int i = 0; i < 5; i++)
    Console.WriteLine(rnd2.Next());

rnd1 = new Random(Guid.NewGuid().GetHashCode());
rnd2 = new Random(Guid.NewGuid().GetHashCode());
Console.WriteLine("First 5 random number in rnd1 using Guid");
for (int i = 0; i < 5; i++)
    Console.WriteLine(rnd1.Next());
Console.WriteLine("First 5 random number in rnd2 using Guid");
for (int i = 0; i < 5; i++)
    Console.WriteLine(rnd2.Next());
```

Another way to achieve different seeds is to use another Random instance to retrieve the seed values.

```
Random rndSeeds = new Random();
Random rnd1 = new Random(rndSeeds.Next());
Random rnd2 = new Random(rndSeeds.Next());
```

This also makes it possible to control the result of all the Random instances by setting only the seed value for the rndSeeds. All the other instances will be deterministically derived from that single seed value.

# Section 149.5: Generate a Random double

Generate a random number between 0 and 1.0. (not including 1.0)

```
Random rnd = new Random();
var randomDouble = rnd.NextDouble();
```

# Section 149.6: Generate a random character

Generate a random letter between a and z by using the Next() overload for a given range of numbers, then converting the resulting int to a char

```
Random rnd = new Random();
char randomChar = (char)rnd.Next('a','z');
// 'a' and 'z' are interpreted as ints for parameters for Next()
```

# Section 149.7: Generate a number that is a percentage of a max value

A common need for random numbers it to generate a number that is X% of some max value. this can be done by treating the result of NextDouble() as a percentage: