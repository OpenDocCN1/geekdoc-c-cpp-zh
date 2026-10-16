
{
    foreach (var filename in input.GetConsumingEnumerable())
    {
        using (FileStream stream = File.OpenRead(filename))
        {
            var reader = new StreamReader(stream);
            string line = null;
            while ((line = await reader.ReadLineAsync()) != null)
            {
                output.Add(line);
                ColoredConsole.WriteLine($"stage 2: added {line}");
            }
        }
    }
    output.CompleteAdding();
}

> NOTE If a reader is reading a collection at the same time while it is filled, you need to get the enumerator of the blocking collection with the method GetConsumingEnumerable instead of iterating the collection directly.

### Using a ConcurrentDictionary

Stage 3 is implemented in the ProcessContentAsync method. This method gets the lines from the input collection, and then splits and filters words to an output dictionary. The method AddOrUpdate is a method from the ConcurrentDictionary type. If the key is not yet added to the dictionary, the second parameter defines the value that should be set. If the key is already available in the dictionary, the updateValueFactory parameter defines how the value should be changed. In this case, the existing value is just incremented by one:

```
public static Task ProcessContentAsync(
    BlockingCollection<string> input,
    ConcurrentDictionary<string, int> output)
{
    return Task.Factory.StartNew(() =>
    {
        foreach (var line in input.GetConsumingEnumerable())
        {
            string[] words = line.Split(' ', ';', '\t', '{', '}', '(', ')', ':', ',', '"');
            foreach (var word in words.Where(w => !string.IsNullOrEmpty(w)))
            {
                output.AddOrUpdate(key: word, addValue: 1, updateValueFactory: (s, i) => ++i);
                ColoredConsole.WriteLine($"stage 3: added {word}");
            }
        }
    }, TaskCreationOptions.LongRunning);
}
```

Running the application with the first three stages, you’ll see output like the following, where the stages operate interleaved:

```
stage 3: added DisplayBits
stage 3: added bits2
stage 3: added Write
stage 3: added =
stage 3: added bits1.Or
stage 2: added             DisplayBits(bits2);
stage 2: added             Write(" and");
stage 2: added             DisplayBits(bits1);
stage 2: added             WriteLine();
stage 2: added             DisplayBits(bits2);
```

### Completing the Pipeline

After the first three stages are completed, the next three stages can run in parallel again. TransferContentAsync gets the data from the dictionary, converts it to the type Info, and puts it into the output `BlockingCollection<T>` (code file PipelineSample/PipelineStages.cs):

```
public static Task TransferContentAsync(
    ConcurrentDictionary<string, int> input,
    BlockingCollection<Info> output)
{
    return Task.Factory.StartNew(() =>
    {
        foreach (var word in input.Keys)
        {
            int value;
            if (input.TryGetValue(word, out value))
            {
                var info = new Info { Word = word, Count = value };
                output.Add(info);
                ColoredConsole.WriteLine($"stage 4: added {info}");
            }
        }
        output.CompleteAdding();
    }, TaskCreationOptions.LongRunning);
}
```

The pipeline stage AddColorAsync sets the Color property of the Info type depending on the value of the Count property:

```
public static Task AddColorAsync(BlockingCollection<Info> input,
    BlockingCollection<Info> output)
{
    return Task.Factory.StartNew(() =>
    {
        foreach (var item in input.GetConsumingEnumerable())
        {
            if (item.Count > 40)
            {
                item.Color = "Red";
            }
            else if (item.Count > 20)
            {
                item.Color = "Yellow";
            }
            else
            {
                item.Color = "Green";
            }
            output.Add(item);
            ColoredConsole.WriteLine($"stage 5: added color {item.Color} to {item}");
```

## 13 Language Integrated Query

### What’s In This Chapter?

- Traditional queries across objects using List
- Extension methods
- LINQ query operators
- Parallel LINQ
- Expression trees

### Wrox.com Code Downloads for This Chapter

The wrox.com code downloads for this chapter are found at www.wrox.com/go/professionalcsharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

- LINQ Intro
- Enumerable Sample
- Parallel LINQ
- Expression Trees

### LINQ Overview

LINQ (Language Integrated Query) integrates query syntax inside the C# programming language, making it possible to access different data sources with the same syntax. LINQ accomplishes this by offering an abstraction layer.

This chapter describes the core principles of LINQ and the language extensions for C# that make the C# LINQ Query possible.

> NOTE For details about using LINQ across the database, you should read Chapter 38, “Entity Framework Core.” For information about querying XML data, read Chapter 27, “XML and JSON,” after reading this chapter.

This chapter starts with a simple LINQ query before diving into the full potential of LINQ. The C# language offers an integrated query language that is converted to method calls. This section shows you what the conversion looks like so you can use all the possibilities of LINQ.

### Lists and Entities

The LINQ queries in this chapter are performed on a collection containing Formula-1 champions from 1950 to 2015. This data needs to be prepared with entity classes and lists.

For the entities, the type `Racer` is defined. `Racer` defines several properties and an overloaded `ToString` method to display a racer in a string format. This class implements the interface `IFormattable` to support different variants of format strings, and the interface `IComparable<Racer>`, which can be used to sort a list of racers based on the `LastName`. For more advanced queries, the class `Racer` contains not only single-value properties such as `FirstName`, `LastName`, `Wins`, `Country`, and `Starts`, but also properties that contain a collection, such as `Cars` and `Years`. The `Years` property lists all the years of the championship title. Some racers have won more than one title. The `Cars` property is used to list all the cars used by the driver during the title years (code file `DataLib/Racer.cs`):

```
using System;
using System.Collections.Generic;

namespace Wrox.ProCSharp.LINQ
{
    public class Racer : IComparable<Racer>, IFormattable
    {
        public Racer(string firstName, string lastName, string country,
                     int starts, int wins)
            : this(firstName, lastName, country, starts, wins, null,
                   null)
        {
        }

        public Racer(string firstName, string lastName, string country,
                     int starts, int wins, IEnumerable<int> years,
                     IEnumerable<string> cars)
        {
            FirstName = firstName;
            LastName = lastName;
            Country = country;
            Starts = starts;
            Wins = wins;
            Years = years != null ? new List<int>(years) : new List<int>();
            Cars = cars != null ? new List<string>(cars) : new List<string>();
        }

        public string FirstName { get; set; }
        public string LastName { get; set; }
        public int Wins { get; set; }
        public string Country { get; set; }
        public int Starts { get; set; }
        public IEnumerable<string> Cars { get; }
        public IEnumerable<int> Years { get; }

        public override string ToString() => $"{FirstName} {LastName}";

        public int CompareTo(Racer other) => LastName.CompareTo(other?.LastName);

        public string ToString(string format) => ToString(format, null);

        public string ToString(string format, IFormatProvider formatProvider)
        {
            switch (format)
            {
                case null:
                case "N":
                    return ToString();
                case "F":
                    return FirstName;
                case "L":
                    return LastName;
                case "C":
                    return Country;
                case "S":
                    return Starts.ToString();
                case "W":
                    return Wins.ToString();
                case "A":
                    return $"{FirstName} {LastName}, {Country}; starts: {Starts}, wins: {Wins}";
                default:
                    throw new FormatException($"Format {format} not supported");
            }
        }
    }
}
```

A second entity class is Team. This class just contains the name and an array of years for constructor championships. Similar to a driver championship, there’s a constructor championship for the best team of a year (code file `DataLib/Team.cs`):

```
public class Team
{
    public Team(string name, params int[] years)
    {
        Name = name;
        Years = years != null ? new List<int>(years) : new List<int>();
    }
    public string Name { get; }
    public IEnumerable<int> Years { get; }
}
```

The class Formula1 returns a list of racers in the method GetChampions. The list is filled with all Formula-1 champions from the years 1950 to 2015 (code file `DataLib/Formula1.cs`):

```
using System.Collections.Generic;

namespace Wrox.ProCSharp.LINQ
{
    public static class Formula1
    {
        private static List<Racer> _racers;

        public static IList<Racer> GetChampions()
        {
            if (_racers == null)
```
