
Similar to classes, structs can be generic as well. They are very similar to generic classes with the exception of inheritance features. In this section you look at the generic struct Nullable<T>, which is defined by the .NET Framework.

An example of a generic struct in the .NET Framework is Nullable<T>. A number in a database and a number in a programming language have an important difference: A number in the database can be null, whereas a number in C# cannot be null. Int32 is a struct, and because structs are implemented as value types, they cannot be null. This difference often causes headaches and a lot of additional work to map the data. The problem exists not only with databases but also with mapping XML data to .NET types.

One solution is to map numbers from databases and XML files to reference types, because reference types can have a null value. However, this also means additional overhead during runtime.

With the structure Nullable<T>, this can be easily resolved. The following code segment shows a simplified version of how Nullable<T> is defined. The structure Nullable<T> defines a constraint specifying that the generic type T needs to be a struct. With classes as generic types, the advantage of low overhead is eliminated; and because objects of classes can be null anyway, there’s no point in using a class with the Nullable<T> type. The only overhead in addition to the T type defined by Nullable<T> is the hasValue Boolean field that defines whether the value is set or null. Other than that, the generic struct defines the read-only properties HasValue and Value and some operator overloads. The operator overload to cast the Nullable<T> type to T is defined as explicit because it can throw an exception in case hasValue is false. The operator overload to cast to Nullable<T> is defined as implicit because it always succeeds:

```
public struct Nullable<T>
    where T: struct
{
    public Nullable(T value)
    {
        _hasValue = true;
        _value = value;
    }
    private bool _hasValue;
    public bool HasValue => _hasValue;

    private T _value;
    public T Value
    {
        get
        {
            if (!_hasValue)
            {
                throw new InvalidOperationException("no value");
            }
            return _value;
        }
    }

    public static explicit operator T(Nullable<T> value) => value.Value;

    public static implicit operator Nullable<T>(T value) => new Nullable<T>(value);

    public override string ToString() => !HasValue ? string.Empty : _value.ToString();
}
```

In this example, Nullable<T> is instantiated with Nullable<int>. The variable x can now be used as an int, assigning values and using operators to do some calculation. This behavior is made possible by casting operators of the Nullable<T> type. However, x can also be null. The Nullable<T> properties HasValue and Value can check whether there is a value, and the value can be accessed:

```
Nullable<int> x;
x = 4;
x += 3;
if (x.HasValue)
{
    int y = x.Value;
}
x = null;
```

Because nullable types are used often, C# has a special syntax for defining variables of this type. Instead of using syntax with the generic structure, the ? operator can be used. In the following example, the variables x1 and x2 are both instances of a nullable int type:

```
Nullable<int> x1;
int? x2;
```

A nullable type can be compared with null and numbers, as shown. Here, the value of x is compared with null, and if it is not null it is compared with a value less than 0:

```
int? x = GetNullableType();
if (x == null)
{
    WriteLine("x is null");
}
else if (x < 0)
{
    WriteLine("x is smaller than 0");
}
```

Now that you know how Nullable<T> is defined, let’s get into using nullable types. Nullable types can also be used with arithmetic operators. The variable x3 is the sum of the variables x1 and x2. If any of the nullable types have a null value, the result is null:

```
int? x1 = GetNullableType();
int? x2 = GetNullableType();
int? x3 = x1 + x2;
```

> **NOTE** The GetNullableType method, which is called here, is just a placeholder for any method that returns a nullable int. For testing you can implement it to simply return null or to return any integer value.

Non-nullable types can be converted to nullable types. With the conversion from a non-nullable type to a nullable type, an implicit conversion is possible where casting is not required. This type of conversion always succeeds:

```
int y1 = 4;
int? x1 = y1;
```

In the reverse situation, a conversion from a nullable type to a non-nullable type can fail. If the nullable type has a null value and the null value is assigned to a non-nullable type, then an exception of type InvalidOperationException is thrown. That’s why the cast operator is required to do an explicit conversion:

```
int? x1 = GetNullableType();
int y1 = (int)x1;
```

Instead of doing an explicit cast, it is also possible to convert a nullable type to a non-nullable type with the coalescing operator. The coalescing operator uses the syntax ?? to define a default value for the conversion in case the nullable type has a value of null. Here, y1 gets a 0 value if x1 is null:

```
int? x1 = GetNullableType();
int y1 = x1 ?? 0;
```

## Generic Methods

In addition to defining generic classes, it is also possible to define generic methods. With a generic method, the generic type is defined with the method declaration. Generic methods can be defined within non-generic classes.

The method Swap<T> defines T as a generic type that is used for two arguments and a variable temp:

```
void Swap<T>(ref T x, ref T y)
{
    T temp;
    temp = x;
    x = y;
    y = temp;
}
```

A generic method can be invoked by assigning the generic type with the method call:

```
int i = 4;
int j = 5;
Swap<int>(ref i, ref j);
```

However, because the C# compiler can get the type of the parameters by calling the Swap method, it is not necessary to assign the generic type with the method call. The generic method can be invoked as simply as non-generic methods:

```
int i = 4;
int j = 5;
Swap(ref i, ref j);
```

### Generic Methods Example

This example uses a generic method to accumulate all the elements of a collection. To show the features of generic methods, the following Account class, which contains Name and Balance properties, is used (code file GenericMethods/Account.cs):

> **NOTE** With .NET Core, this sample needs a reference to the NuGet package System.Collections.

```
public class Account
{
    public string Name { get; }
    public decimal Balance { get; private set; }
    public Account(string name, Decimal balance)
    {
        Name = name;
        Balance = balance;
    }
}
```

All the accounts in which the balance should be accumulated are added to an accounts list of type List<Account> (code file GenericMethods/Program.cs):

```
var accounts = new List<Account>
{
    new Account("Christian", 1500),
    new Account("Stephanie", 2200),
    new Account("Angela", 1800),
    new Account("Matthias", 2400)
};
```

A traditional way to accumulate all Account objects is by looping through them with a foreach statement, as shown here. Because the foreach statement uses the IEnumerable interface to iterate the elements of a collection, the argument of the AccumulateSimple method is of type IEnumerable. The foreach statement works with every object implementing IEnumerable. This way, the AccumulateSimple method can be used with all collection classes that implement the interface IEnumerable<Account>. In the implementation of this method, the property Balance of the Account object is directly accessed (code file GenericMethods/Algorithms.cs):

```
public static class Algorithms
{
    public static decimal AccumulateSimple(IEnumerable<Account> source)
    {
        decimal sum = 0;
        foreach (Account a in source)
        {
            sum += a.Balance;
        }
        return sum;
    }
}
```

The AccumulateSimple method is invoked like this:

```
decimal amount = Algorithms.AccumulateSimple(accounts);
```

### Generic Methods with Constraints

The problem with the first implementation is that it works only with Account objects. This can be avoided by using a generic method.

The second version of the Accumulate method accepts any type that implements the interface IAccount. As you saw earlier with generic classes, you can restrict generic types with the where clause. You can use the same clause with generic methods that you use with generic classes. The parameter of the Accumulate method is changed to IEnumerable<T>, a generic interface that is implemented by generic collection classes (code file GenericMethods/Algorithms.cs):

```
public static decimal Accumulate<TAccount>(IEnumerable<TAccount> source)
        where TAccount : IAccount
{
    decimal sum = 0;

    foreach (TAccount a in source)
    {
        sum += a.Balance;
    }
    return sum;
}
```

The Account class is now refactored to implement the interface IAccount (code file GenericMethods/Account.cs):

```
public class Account : IAccount
{
    //...
}
```

The IAccount interface defines the read-only properties Balance and Name (code file GenericMethods/IAccount.cs):

```
public interface IAccount
{
    decimal Balance { get; }
    string Name { get; }
}
```

The new Accumulate method can be invoked by defining the Account
