```
```java
Locale::getDisplayCountry,
l -> Collections.singleton(l.getDisplayLanguage()),
(a, b) ->
    { // Union of a and b
        Set<String> union = new HashSet<>(a);
        union.addAll(b);
        return union;
    });
```
```

You will see a simpler way of obtaining this map in the next section.

If you want a TreeMap, supply the constructor as the fourth argument. You must provide a merge function. Here is one of the examples from the beginning of the section, now yielding a TreeMap:

```
```java
Map<Integer, Person> idToPerson = people.collect(
    Collectors.toMap(
        Person::getId,
        Function.identity(),
        (existingValue, newValue) -> { throw new IllegalStateException(); },
        TreeMap::new));
```
```

> **NOTE:** For each of the `toMap` methods, there is an equivalent `toConcurrentMap` method that yields a concurrent map. A single concurrent map is used in the parallel collection process. When used with a parallel stream, a shared map is more efficient than merging maps. Note that elements are no longer collected in stream order, but that doesn’t usually make a difference.

The example program in Listing 1.5 gives examples of collecting stream results into maps.

# **Listing 1.5** `collecting/CollectingIntoMaps.java`

```
```java
package collecting;

import java.io.*;
import java.util.*;
import java.util.function.*;
import java.util.stream.*;

public class CollectingIntoMaps
{
    public static class Person
    {
        private int id;
        private String name;
```
```

*(Continues)*