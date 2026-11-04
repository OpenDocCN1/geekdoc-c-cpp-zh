Although this works just fine, it makes tooling harder, and (what ought to be) properties are clustered together in the method list. Because get and set accessor pairs are such an established concept, .NET made them first-class metadata citizens.

Figure 11.13 shows a property definition in our much beloved ILDASM tool. As you can see, there are methods for the accessors that use get and set prefixes. In addition, a property acts as a piece of metadata that bundles those two methods together. Code that uses a property’s getter or setter uses a direct method call to the respective methods. The metadata is simply there for tooling and services like serialization.

![](bbox=[0.081, 0.284, 0.508, 0.578])

FIGURE 11.13  Dissection of a property.

# Indexers

Closely related to properties are indexers. Both classes and structs can contain just one indexer, which is best described as a parameterized property that can be invoked by using an indexing expression. The stereotypical example of an indexer is on a vector object or a dictionary collection. Let’s first show how the latter is used on the generic Dictionary type defined in System.Collections.Generic and then move on to defining our own Vector type with an indexer:

```
var phoneBook = new Dictionary<string, int>();
phoneBook["Bart"] = 51662;
phoneBook["John"] = 96207;
Console.WriteLine("Bart's phone number is: " + phoneBook["Bart"]);
```

The second and third lines add entries to the dictionary by passing the intended key as a parameter to the indexing expression and by assigning to it. On the fourth line, we read