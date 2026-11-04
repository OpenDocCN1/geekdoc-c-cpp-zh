
Use of properties is recommended over publicly accessible fields because use of fields limits a type's capability to evolve the internal storage structure without breaking the type's users. Properties provide you with a level of indirection (encapsulation) when accessing fields (or small computations derived from it).

Concerning exceptions, it's fine for property accessors to throw exceptions. The most common case where this is used is to validate the value coming in to a property set method, which is just like any other public input that should be validated:

```
public string Name
{
    get { return _name; }
    set
    {
        if (string.IsNullOrEmpty(value))
            throw new ArgumentNullException("value");
        _name = value;
    }
}
```

## "CONSTITUENT TYPES" AND VISIBILITY

Although we've discussed accessibility in various contexts already, we haven't told the whole story yet. A member's constituent types are the set of types that appear in that member's declaration, such as a property type or a method's return types and its parameter types.

It's not permitted to have constituent types that are less accessible than the declaring member itself. For example, a public method cannot take in an object of a type that's not publicly accessible. If it were to, how could a user invoke the method? As an exercise, try to expose an internal Address type through a property's return type and observe the compiler error that ensues.

## Auto-Implemented Properties

![](img/a16f85e62ce9bdc527f4b09dbfe26092_601_0.png)

C# 3.0 introduced a feature called auto-implemented properties to reduce the “smartass ceremony” involved in creating “simple properties” that are nothing but smart fields. Instead of having to declare the backing field and a property accessing that field manually, the following syntax takes care of it all:

```
class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```

The preceding code is turned into this equivalent:

```csharp
class Person
{
    private string <Name>k__BackingField;
    private int <Age>k__BackingField;

    public string Name
    {
        get { return <Name>k__BackingField; }
        set { <Name>k__BackingField = value; }
    }

    public int Age
    {
        get { return <Age>k__BackingField; }
        set { <Age>k__BackingField = value; }
    }
}
```

Although the accessibility of the generated get and set accessor can be specified, it's not possible to declare the backing fields as read-only. I hope that this little feature omission gets rectified in a future release of the language, maybe as part of larger immutability crusades undertaken by the language designers. Auto-implemented properties can easily be inserted in Visual Studio by using the prop snippet. Type prop and press Tab twice, as shown in Figure 11.12.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_602_0.png)

FIGURE 11.12 Auto-implemented property snippet in Visual Studio 2010.

## How Properties Work

Properties are nothing but one or two accessor *methods* that are grouped together by a piece of metadata. This allows code editors and runtime services like reflection to see them as a unique kind of member. Some other languages don't have such a first-class treatment for concepts like properties (and indexers, and events, and so on) and rely on some naming convention instead:

```csharp
class Person
{
    public string getName() { ... }
    public void setName(string name) { ... }
}
```

Although this works just fine, it makes tooling harder, and (what ought to be) properties are clustered together in the method list. Because get and set accessor pairs are such an established concept, .NET made them first-class metadata citizens.

Figure 11.13 shows a property definition in our much beloved ILDASM tool. As you can see, there are methods for the accessors that use get and set prefixes. In addition, a property acts as a piece of metadata that bundles those two methods together. Code that uses a property’s getter or setter uses a direct method call to the respective methods. The metadata is simply there for tooling and services like serialization.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_603_0.png)

FIGURE 11.13  Dissection of a property.

## Indexers

Closely related to properties are indexers. Both classes and structs can contain just one indexer, which is best described as a parameterized property that can be invoked by using an indexing expression. The stereotypical example of an indexer is on a vector object or a dictionary collection. Let’s first show how the latter is used on the generic Dictionary type defined in System.Collections.Generic and then move on to defining our own Vector type with an indexer:

```
var phoneBook = new Dictionary<string, int>();
phoneBook["Bart"] = 51662;
phoneBook["John"] = 96207;
Console.WriteLine("Bart's phone number is: " + phoneBook["Bart"]);
```

The second and third lines add entries to the dictionary by passing the intended key as a parameter to the indexing expression and by assigning to it. On the fourth line, we read an entry from the dictionary. Notice with C# 3.0 collection initializers, you can initialize the dictionary as follows:

```
var phoneBook = new Dictionary<string, int> {
  { "Bart", 51662 },
  { "John", 96207 }
};
```

This doesn't use the indexer but invokes the dictionary's Add method two times, once for each element initialization entry.

## "EVERYTHING SHOULD BE A DICTIONARY"

> In some dynamic languages, the art of indexing is indistinguishable from regular member access. For example, accessing element 0 in an array xs could be xs.0 (not permitted in C#), accessing a member could either be pt.X or pt["X"], and you could simply add members by assigning to a yet-undefined member.
> 
> Starting from C# 4.0, this can be enabled through the use of dynamic and the ExpandoObject type in the System.Dynamic namespace. However, it's my (and my manager's) opinion that static typing should be preferred over dynamic typing whenever possible. You learn more about dynamic later in Chapter 22, "Dynamic Programming."

## Defining Indexers

To define an indexer, you use the this keyword in yet another context. Take a moment to think back about all the allowed uses of this you've seen so far. To see why the this keyword is used in this context, take a closer look at the following code:

```
Vector victor = new Vector(1, 2, 3);
Console.WriteLine("X = " + victor[0]);
// We're leaving the implementation of an indexer with a string-typed parameter
// as an exercise for the reader. (See the next code fragment.)
Console.WriteLine("Y = " + victor["y"]);
Console.WriteLine("Z = " + victor[2]);
```

Because indexing operates on the object directly, there's no member name involved. In fact, from the receiving end's point of view, the left side of the indexing operation is nothing but the object itself, hence this. To define the first indexers taking in an integer parameter, you therefore write the following:

```
class Vector
{
  private int _x, _y, _z;

  public Vector(int x, int y, int z)
{
    _x = x; _y = y; _z = z;
}

public int this[int index]
{
    get
    {
        if (index == 0) return _x;
        else if (index == 1) return _y;
        else if (index == 2) return _z;
        else throw new ArgumentOutOfRangeException();
    }
}
// Insert the implementation of an indexer with a string-typed parameter
// here, allowing the user to write things like vector["x"] or vector["Y"].
}
```

There are different ways to look at it. One is to see the indexer as a property with this as its name, taking in one or more parameters specified between square brackets rather than parentheses. Inside both accessors, those parameters' values are available for use; in the setter, the contextual value keyword receives the incoming object.

For the most part, indexers and properties are similar. One notable difference is that indexers cannot be defined as static members. Also notice that because indexers require at least one parameter (none of which can be ref or out) to be specified at the use site, putting a default value on the first parameter isn't allowed:

```
class Vector
{
    ...
    public int this[int index = 0] { ... }
}
```

If this were permitted, you could write the following, which could be interpreted as quite confusing (compared to array-creation expressions):

```
Vector v;
int x = v[];
```

I leave it as an exercise for you to define a set accessor on the preceding indexer and to implement the setter that takes in a string parameter that specifies the axis using letters x, y, or z.
