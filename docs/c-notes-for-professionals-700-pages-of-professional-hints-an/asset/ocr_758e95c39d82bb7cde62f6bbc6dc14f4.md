# Section 28.2: Do - While Loop

It is similar to a while loop, except that it tests the condition at the end of the loop body. The Do - While loop executes the loop once irrespective of whether the condition is true or not.

```
int[] numbers = new int[] { 6, 7, 8, 10 };

// Sum values from the array until we get a total that's greater than 10,
// or until we run out of values.
int sum = 0;
int i = 0;
do
{
    sum += numbers[i];
    i++;
} while (sum <= 10 && i < numbers.Length);

System.Console.WriteLine(sum); // 13
```

# Section 28.3: Foreach Loop

foreach will iterate over any object of a class that implements IEnumerable (take note that IEnumerable<T> inherits from it). Such objects include some built-in ones, but not limit to: List<T>, T[] (arrays of any type), Dictionary<TKey, TValue>, as well as interfaces like IQueryable and ICollection, etc.

# syntax

```
foreach(ItemType itemVariable in enumerableObject)
    statement;
```

# remarks

+   1. The type ItemType does not need to match the precise type of the items, it just needs to be assignable from the type of the items
+   2. Instead of ItemType, alternatively var can be used which will infer the items type from the enumerableObject by inspecting the generic argument of the IEnumerable implementation
+   3. The statement can be a block, a single statement or even an empty statement (;)
+   4. If enumerableObject is not implementing IEnumerable, the code will not compile
+   5. During each iteration the current item is cast to ItemType (even if this is not specified but compiler-inferred via var) and if the item cannot be cast an InvalidCastException will be thrown.

Consider this example:

```
var list = new List<string>();
list.Add("Ion");
list.Add("Andrei");
foreach(var name in list)
{
    Console.WriteLine("Hello " + name);
}
```

is equivalent to:

```
var list = new List<string>();
list.Add("Ion");
list.Add("Andrei");
```