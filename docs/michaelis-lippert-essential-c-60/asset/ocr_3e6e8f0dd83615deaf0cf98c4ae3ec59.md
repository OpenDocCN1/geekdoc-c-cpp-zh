Listing 14.12 also provides a selection of sample data. Output 14.2 displays the results of running this code.

# OUTPUT 14.2

```
Bifocals (1784)
Phonograph (1877)
Kinetoscope (1888)
Electrical Telegraph (1837)
Flying Machine (1903)
Steam Locomotive (1815)
Droplet Deposition Apparatus (1789)
Backless Brassiere (1914)

Benjamin Franklin (Philadelphia, PA)
Orville Wright (Kitty Hawk, NC)
Wilbur Wright (Kitty Hawk, NC)
Samuel Morse (New York, NY)
George Stephenson (Wylam, Northumberland)
John Michaelis (Chicago, IL)
Mary Phelps Jacob (New York, NY)
```

# Filtering with Where()

To filter out data from a collection, we need to provide a filter method that returns true or false, indicating whether a particular element should be included or not. A delegate expression that takes an argument and returns a Boolean is called a predicate, and a collection’s Where() method depends on predicates for identifying filter criteria, as shown in Listing 14.13. (Technically, the result of the Where() method is a monad that encapsulates the operation of filtering a given sequence with a given predicate.) The results appear in Output 14.3.

# LISTING 14.13: Filtering with System.Linq.Enumerable.Where()

```
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        IEnumerable<Patent> patents = PatentData.Patents;
        patents = patents.Where(
            patent => patent.YearOfPublication.StartsWith("18"));
        Print(patents);
    }

    // ...
}
```