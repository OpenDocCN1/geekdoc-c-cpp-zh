
![](img/a16f85e62ce9bdc527f4b09dbfe26092_794_0.png)

FIGURE 16.6 References in LinkedList<T> and LinkedListNode<T>.

An example of creating and manipulating a list is shown here:

```csharp
var lst = new LinkedList<string>();

var elem1 = lst.AddFirst("isn't");
var elem2 = lst.AddBefore(elem1, "This");
var elem3 = lst.AddAfter(elem1, "a");
var elem4 = lst.AddLast("list");
var elem5 = lst.AddBefore(elem4, "singly");
var elem6 = lst.AddAfter(elem5, "linked");

lst.Last.Previous.Previous.Value = "doubly";
lst.First.Next.Value = "is";

foreach (var word in lst)
    Console.Write(word + " ");

Console.WriteLine();
```

Notice all operations that manipulate the list take place through the LinkedList<T> type. This enables the list to maintain the list structure in a consistent manner, keeping all Next and Previous references in a good state. Similarly, adding an element in front of the first element requires the First reference to be updated to point at the new “head” of the list.
Adding an element after the last one requires an update of the Last reference.

When walking the list manually by following Next or Previous references, be aware that the list is not circular. Null references indicate that the end or beginning of the list has been reached. In other words, First.Previous and Last.Next will always return null.

### THE CASE OF THE BROKEN COLLECTION INITIALIZER

`LinkedList<T>` doesn't support the handy C# 3.0 collection initializer syntax.
Looking at the type's interface implementation list, you might think it should; after all, it implements the `ICollection` interface, which has an `Add` method on it, right? However, this collection type implements that interface explicitly, thus making the `Add` method private on the class itself. Therefore, the compiler doesn't find an `Add` method to call for the collection initializer's use. The following works, though:

```csharp
var lst = new LinkedList<string>();
((ICollection<string>)lst).Add("Hello"); // calling through the interface
```

So the duck-typed nature of collection initializers with regard to discovering an `Add` method sometimes (but rarely ever) works against the feature.

## `Dictionary<TKey, TValue>`

To provide a generically typed alternative to `Hashtable`, the `Dictionary<TKey, TValue>` type was invented. Where `Hashtable` uses `System.Object` for both its keys and values, the generic dictionary allows static typing of keys and values. Let's cross-translate our original example again:

```csharp
var tbl = new Dictionary<string, int>();
tbl.Add("Bart", 26);
tbl["John"] = 62;

bool bartIsKnown = tbl.ContainsKey("Bart");
bool someIsAged62 = tbl.ContainsValue(62);
foreach (var name in tbl.Keys)
    Console.WriteLine("Age of {0} is {1}", name, tbl[name]);

tbl.Remove("Bart");
```

The code still looks exactly the same, thanks to the mirrored API design compared to `Hashtable`. This makes people with prior experience using `Hashtable` feel at home immediately in the world of generic dictionaries. The obvious difference is you can't make any typing mistakes anymore. This is illustrated once more in Figure 16.7, also showing how IntelliSense guides you in the right direction.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_796_0.png)

FIGURE 16.7 Stronger type checking enforced by generics.

Notice how the example uses an implicitly typed local variable for the foreach loop’s iteration variable. Because all type information around generics is known at compile time, as proven by the great IntelliSense experience, the compiler can infer statically what the loop variable’s type ought to be. This is proven by code editor inspection in Figure 16.8.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_796_1.png)

FIGURE 16.8 Rich type information available at compile time.

While we’re at it, direct iteration over dictionary types (as opposed to going over keys or values individually) is also possible. By looking at the definition of the generic type, you can trace why this is the case:

```csharp
public class Dictionary<TKey, TValue> : IDictionary<TKey, TValue>, ...
```

From here, we get into the IDictionary<TKey, TValue> generic interface, which in turn leads us to an ICollection generic interface:

```csharp
public interface IDictionary<TKey, TValue> :
    ICollection<KeyValuePair<TKey, TValue>>
```

Here things start to get more interesting: The ICollection<T> interface is parameterized with the KeyValuePair<TKey, TValue> generic type. But first, let’s finish our tracing of the enumerable nature of a generic dictionary by following the ICollection<T> trail:

```csharp
public interface ICollection<T> : IEnumerable<T>
```

To conclude this type-chasing exercise, we've discovered how each generic dictionary type implements IEnumerable<T>, where T is substituted for a KeyValuePair generic constructed type. KeyValuePair<TKey, TValue> is defined like this:

```csharp
public struct KeyValuePair<TKey, TValue> {
    public KeyValuePair(TKey key, TValue value);

    public TKey Key { get; }
    public TValue Value { get; }
}
```

Based on this observation, we can also loop over our dictionary as follows, extracting the name and age values using Key and Value properties:

```csharp
foreach (var entry in tbl)
    Console.WriteLine(entry.Key + " is " + entry.Value);
```

Once more local variable type inference knows exactly what we're talking about, as shown in Figure 16.9.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_797_0.png)

FIGURE 16.9 IDictionary<TKey, TValue> is IEnumerable<KeyValuePair<TKey, TValue>>.

## IMPLICITLY TYPED LOCAL VARIABLES

Although implicitly typed local variables or local variable type inference, using the var keyword, was introduced for use mainly in conjunction with anonymous types, its use extends far beyond that. Generic (collection) types are one of the places where type inference can prove tremendously useful in reducing code clutter. With generic types, large type names can be constructed in no time:

```csharp
Dictionary<string, List<int>> personLottoNumbers
    = new Dictionary<string, List<int>>();
```

Simple object instantiation doesn't even fit on one line anymore because the type has to be stated twice. Even though some programmers have identified the var keyword as the devil in disguise, it's hard to deny the following is cleaner:

```csharp
var personLottoNumbers = new Dictionary<string, List<int>>();
```

Have you lost track of type information? No. Is the code cleaner? Yes. That's a win-win situation if you ask me.

One final method we should examine when talking about this collection type is the handy self-explanatory TryGetValue method:

```csharp
int ageOfMarge;
if (tbl.TryGetValue("Marge", out ageOfMarge))
    // Code if the key was found, with ageOfMarge set to the retrieved value.
```

The generic dictionary type is, just like the Hashtable type, based on hashing to provide efficient lookup of entries by their keys. This implies the same caveats regarding providing a good hash function on the key type and ensuring immutability of key values apply.

Where the Hashtable type uses the System.Object's GetHashCode and Equals virtual methods directly for key object storage, the generic dictionary type introduces one more level of abstraction by means of an IEqualityComparer<T> interface:

```csharp
public interface IEqualityComparer<in T> {
    bool Equals(T x, T y);
    int GetHashCode(T obj);
}
```

Although a custom equality comparer implementation can be provided to the generic dictionary constructor, one typically relies on the default EqualityComparer<T> being used. This one uses the System.Object virtual methods internally to be on par with the default behavior used by the nongeneric Hashtable collection type. Use of a custom equality comparer can come in handy to override the key type's default behavior with regard to hash code calculation and equality checking (for example, to implement non-case-sensitive key differentiation). This is already done by means of a StringComparer type in the .NET Framework:

```csharp
var ages = new Dictionary<string, int>(StringComparer.CurrentCultureIgnoreCase)
{
    { "Homer", 38 },
    { "Bart", 10 }
};
Console.WriteLine(ages["bart"]); // different casing, still works
```
