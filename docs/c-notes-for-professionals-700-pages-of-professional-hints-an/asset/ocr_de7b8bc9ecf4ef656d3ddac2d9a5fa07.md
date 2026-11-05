# ### Section 66.42: GroupJoin with outer range variable

```
```csharp
Customer[] customers = Customers.ToArray();
Purchase[] purchases = Purchases.ToArray();

var groupJoinQuery =
    from c in customers
    join p in purchases on c.ID equals p.CustomerID
    into custPurchases
    select new
    {
        CustName = c.Name,
        custPurchases
    };
```
```

# ### Section 66.43: Linq Quantifiers

Quantifier operations return a Boolean value if some or all of the elements in a sequence satisfy a condition. In this article, we will see some common LINQ to Objects scenarios where we can use these operators. There are 3 Quantifiers operations that can be used in LINQ:

All – used to determine whether all the elements in a sequence satisfy a condition. Eg:

```
```csharp
int[] array = { 10, 20, 30 };

// Are all elements >= 10? YES
array.All(element => element >= 10);

// Are all elements >= 20? NO
array.All(element => element >= 20);

// Are all elements < 40? YES
array.All(element => element < 40);
```
```

Any - used to determine whether any elements in a sequence satisfy a condition. Eg:

```
```csharp
int[] query=new int[] { 2, 3, 4 }
query.Any (n => n == 3);
```
```

Contains - used to determine whether a sequence contains a specified element. Eg:

```
```csharp
//for int array
int[] query =new int[] { 1,2,3 };
query.Contains(1);

//for string array
string[] query={"Tom","grey"};
query.Contains("Tom");

//for a string
var stringValue="hello";
stringValue.Contains("h");
```
```

# ### Section 66.44: TakeWhile

TakeWhile returns elements from a sequence as long as the condition is true