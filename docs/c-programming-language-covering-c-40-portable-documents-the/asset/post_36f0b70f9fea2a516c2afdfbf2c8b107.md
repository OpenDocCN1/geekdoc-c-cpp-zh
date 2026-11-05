
This last overload caused problems, as it does a different thing. For example,

```
"Joshua, Hannah, Joseph".IndexOf("Hannah");// Returns 7
```

but

```
"Joshua, Hannah, Joseph".IndexOf(new char [] {'H','a','n','n','a','h'});
// Returns 3
```

In this case, it would be better to give the overload that does something a different name:

```
public class String {
    public int IndexOf (string value);
    // Returns the index of value within this instance
    public int IndexOf (char value);
    // Returns the index of value within this instance
    public int IndexOfAny(char [] value);
    // Returns the first index of any of the
    // characters in value within the current instance
}
```

> **BILL WAGNER** Method overloading and inheritance don't mix very well. Because overload resolution rules sometimes favor methods declared in the most derived class, that can sometimes mean a method declared in the derived class may be chosen instead of a method that appears to be a better match in the base class. For that reason, I recommend not overloading members that are declared in a base class.

## 1.6.7 Other Function Members

Members that contain executable code are collectively known as the function members of a class. The preceding section describes methods, which are the primary kind of function members. This section describes the other kinds of function members supported by C#: constructors, properties, indexers, events, operators, and destructors.

The following table shows a generic class called List<T>, which implements a growable list of objects. The class contains several examples of the most common kinds of function members.

| Code | Category |
|---|---|
| `public class List<T>`<br>`{` | |
| `const int defaultCapacity = 4;` | Constant |
| `T[] items;`<br>`int count;` | Fields |
| `public List(int capacity = defaultCapacity) {`<br>`    items = new T[capacity];`<br>`}` | Constructors |
| `public int Count {`<br>`    get { return count; }`<br>`}`<br>`public int Capacity {`<br>`    get {`<br>`        return items.Length;`<br>`    }`<br>`    set {`<br>`        if (value < count) value = count;`<br>`        if (value != items.Length) {`<br>`            T[] newItems = new T[value];`<br>`            Array.Copy(items, 0, newItems, 0, count);`<br>`            items = newItems;`<br>`        }`<br>`    }`<br>`}` | Properties |
| `public T this[int index] {`<br>`    get {`<br>`        return items[index];`<br>`    }`<br>`    set {`<br>`        items[index] = value;`<br>`        OnChanged();`<br>`    }`<br>`}` | Indexer |

```csharp
public void Add(T item) {
    if (count == Capacity) Capacity = count * 2;
    items[count] = item;
    count++;
    OnChanged();
}
protected virtual void OnChanged() {
    if (Changed != null) Changed(this, EventArgs.Empty);
}
public override bool Equals(object other) {
    return Equals(this, other as List<T>);
}
static bool Equals(List<T> a, List<T> b) {
    if (a == null) return b == null;
    if (b == null || a.count != b.count) return false;
    for (int i = 0; i < a.count; i++) {
        if (!object.Equals(a.items[i], b.items[i])) {
            return false;
        }
    }
    return true;
}
public event EventHandler Changed;
public static bool operator ==(List<T> a, List<T> b) {
    return Equals(a, b);
}
public static bool operator !=(List<T> a, List<T> b) {
    return !Equals(a, b);
}
```

### 1.6.7.1 Constructors

C# supports both instance and static constructors. An instance constructor is a member that implements the actions required to initialize an instance of a class. A static constructor is a member that implements the actions required to initialize a class itself when it is first loaded.

A constructor is declared like a method with no return type and the same name as the containing class. If a constructor declaration includes a static modifier, it declares a static constructor. Otherwise, it declares an instance constructor.

Instance constructors can be overloaded. For example, the List<T> class declares two instance constructors, one with no parameters and one that takes an int parameter. Instance constructors are invoked using the new operator. The following statements allocate two List<string> instances using each of the constructors of the List class.

```
List<string> list1 = new List<string>();
List<string> list2 = new List<string>(10);
```

Unlike other members, instance constructors are not inherited, and a class has no instance constructors other than those actually declared in the class. If no instance constructor is supplied for a class, then an empty one with no parameters is automatically provided.

> **BRAD ABRAMS** Constructors should be lazy! The best practice is to do minimal work in the constructor—that is, to simply capture the arguments for later use. For example, you might capture the name of the file or the path to the database, but don't open those external resources until absolutely necessary. This practice helps to ensure that possibly scarce resources are allocated for the smallest amount of time possible.
> 
> I was personally bitten by this issue recently with the DataContext class in Linq to Entities. It opens the database in the connection string provided, rather than waiting to perform that operation until it is needed. For my test cases, I was providing test suspect data directly and, in fact, never wanted to open the database. Not only does this unnecessary activity lead to a performance loss, but it also makes the scenario more complicated.

### 1.6.7.2 Properties

Properties are a natural extension of fields. Both are named members with associated types, and the syntax for accessing fields and properties is the same. However, unlike fields, properties do not denote storage locations. Instead, properties have accessors that specify the statements to be executed when their values are read or written.

> **JESSE LIBERTY** A property looks to the creator of the class like a method allowing the developer to add behavior prior to setting or retrieving the underlying value. In contrast, the property appears to the client of the class as if it were a field, providing direct, unencumbered access through the assignment operator.

> **ERIC LIPPERT** A standard "best practice" is to always expose field-like data as properties with getters and setters rather than exposing the field. That way, if you ever want to add functionality to your getter and setter (e.g., logging, data binding, security checking), you can easily do so without "breaking" any consumer of the code that might rely on the field always being there.
> 
> Although in some sense this practice is a violation of another bit of good advice ("Avoid premature generalization"), the new "automatically implemented properties" feature makes it very easy and natural to use properties rather than fields as part of the public interface of a type.

> **CHRIS SELLS** Eric makes such a good point that I wanted to show an example.
> 
> Don't ever make a field public:

```
class Cow
{
    public int Milk; // BAD!
}
```

If you don't want to layer in anything besides storage, let the compiler implement the property for you:

```
class Cow
{
    public int Milk { get; set; } // Good
}
```

That way, the client binds to the property getter and setter so that later you can take over the compiler's implementation to do something fancy:

```
class Cow {
    bool gotMilk = false;
    int milk;
    public int Milk {
        get {
            if (!gotMilk) {
                milk = ApplyMilkingMachine();
                gotMilk = true;
            }
            return milk;
        }
        set {
            ApplyReverseMilkingMachine(value); // The cow might not like this..
            milk = value;
        }
    }
...
```

Also, I really love the following idiom for cases where you know a calculated value will be used in your program:

```
class Cow {
    public Cow() {
        Milk = ApplyMilkingMachine();
    }

    public int Milk { get; private set; }
    ...
}
```

In this case, we are precalculating the property, which is a waste if we don't know whether we will need it. If we do know, we save ourselves some complication in the code by eliminating a flag, some branching logic, and the storage management.

> BILL WAGNER Property accesses look like field accesses to your users—and they will naturally expect them to act like field accesses in every way, including performance. If a get accessor needs to do significant work (reading a file or querying a database, for example), it should be exposed as a method, not a property. Callers expect that a method may be doing more work.
> 
> For the same reason, repeated calls to property accessors (without intervening code) should return the same value. DateTime.Now is one of very few examples in the framework that does not follow this advice.

A property is declared like a field, except that the declaration ends with a get accessor and/or a set accessor written between the delimiters { and } instead of ending in a semi-colon. A property that has both a get accessor and a set accessor is a read-write property, a property that has only a get accessor is a read-only property, and a property that has only a set accessor is a write-only property.

A get accessor corresponds to a parameterless method with a return value of the property type. Except as the target of an assignment, when a property is referenced in an expression, the get accessor of the property is invoked to compute the value of the property.
