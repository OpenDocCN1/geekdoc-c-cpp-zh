and last name are sorted by the account balance. This is why the list of accounts under the name Jones is shown in this order:

```
```
Jones, Jenny        Acc#: 108CK,      $10.98

Jones, Ralph        Acc#: 434CK,      ($123.32)
Jones, Ralph        Acc#: 454MM,       $987.13
Jones, Ralph        Acc#: 436CD,      $1,923.85
```
```

As the output confirms, the list is sorted by last name, then by first name, and finally by account balance.

When using multiple criteria, you can reverse the condition of any sort by applying the *descending* option. For example, this query causes the results to be shown in order of decreasing balance:

```
```csharp
var accInfo = from acc in accounts
              orderby x.LastName, x.FirstName, x.Balance descending
              select acc;
```
```

When using this version, the list of Jones entries will be displayed like this:

```
```
Jones, Jenny        Acc#: 108CK,      $10.98

Jones, Ralph        Acc#: 436CD,      $1,923.85
Jones, Ralph        Acc#: 454MM,       $987.13
Jones, Ralph        Acc#: 434CK,      ($123.32)
```
```

As you can see, now the accounts for Ralph Jones are displayed from greatest to least.

# ## A Closer Look at **select**

The **select** clause determines what type of elements are obtained by a query. Its general form is shown here:

```
```
select expression
```
```

So far we have been using **select** to return the range variable. Thus, *expression* has simply named the range variable. However, **select** is not limited to this simple action. It can return a specific portion of the range variable, the result of applying some operation or transformation to the range variable, or even a new type of object that is constructed from pieces of the information retrieved from the range variable. This is called *projecting*.

To begin examining the other capabilities of **select**, consider the following program. It displays the square roots of the positive values contained in an array of **double** values.

```
```csharp
// Use select to return the square root of all positive values
// in an array of doubles.
using System;
using System.Linq;

class SelectDemo {

    static void Main() {
```
```