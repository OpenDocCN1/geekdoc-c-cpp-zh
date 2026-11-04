
Because the < and > tokens were used only for comparison before, using them for generic parameters had the potential to break things. Does the preceding code mean that the user wants to call a method F with two parameters that result from comparing G and A, and B and the constant 4? That's plausible, but with generics the user may have meant to call F with the result of calling generic method G using type parameters A and B and an argument of 4. If this fascinates you, take a look at the language specification to get the answer on the language's interpretation.

## foreach Analogy

If you're entirely new to LINQ, it helps to think about the from clause as if it were the same as foreach. Ultimately, queries execute with some iterative feeling, and the syntactical analogy is striking (which isn't a coincidence). For example:

```
var nums = new ArrayList { 1, 2, 3, 4, 5 };
from int n in nums ...
```

This is similar to the following:

```
var nums = new ArrayList { 1, 2, 3, 4, 5 };
foreach (int n in nums) {
...
}
```

From an operational point of view, this analogy holds to some extent, enough to help people reason about the query. But there are quite a few differences. The foreach loop is a statement and therefore doesn't produce a value, whereas the query expression is, well, an expression and therefore produces a value. Second, because the foreach loop is imperative, it executes on the spot, whereas a LINQ query is evaluated lazily, as explained in Chapter 20 in the section, "Iterators."

## Multiple Sources

More-complex queries often require more than one data source to query from at the same time. If you reason aloud in terms of "for every element in the first source," on to "for every related element in the second source," nested from clauses are what you need. Making the comparison with the foreach statement is useful again because this looks exactly like nested loops. Here's an example:

```
from product in products
from order in product.Orders
```

Here we assume products is a source with Product objects, with an Orders property defined on the Products class. Orders returns a collection of Order objects. In other words, we're querying the orders for every product.

What this turns into internally is something discussed in much detail in Chapter 20 in the section, “Projection,” but to convince you LINQ syntax always boils down to method calls, here’s one possibility:

```
products.SelectMany(product => product.Orders, (product, order) => ...)
...
```

In fact, SelectMany is implemented using nested foreach loops. All that matters now is that you can have multiple sources that are being used inside the query expression. Conceptually, you can think of them as nested loops.

## DIFFERENT SOURCES, DIFFERENT APPROACHES

Dealing with different data sources can be done in different ways. Maybe you want to create the Cartesian product of two sources and execute the rest of the query for each couple of elements from both sources. This is achievable through the use of multiple from clauses, in particular when the sources are independent:

```
from x in xs
from y in ys // ys is not dependent on x
// I can use x and y here
```

Sometimes the second source depends on the element that comes out of the first one, as shown in the products and orders preceding example, which is quite different.

Finally, you might want to combine elements from two sources pair-wise. For example, if you have { 1, 2 } and { 3, 4 }, you want to get with { (1,3), (2,4) }. This can be achieved using the new .NET 4.0 standard query operator Zip, discussed in the next chapter in the section, “Zip.”

## Projection Using the Select Clause

Now that we’ve identified the query sources, we can start operating on the data they provide. Although you might think of filtering and ordering as the first kind of operations you want to perform, we’ll start from the end. Every query expression in C# needs to end either by a select clause or a group by clause. The former operation is the simplest to explain so we start from there.

## Identity Projection

The most trivial projection possible doesn’t do any transformation on the input data and is called the identity projection, after the identity function. An example is shown here:

```
var nums = new List<int> { 1, 2, 3, 4, 5 };
var res = from n in nums
    select n;
```

This will produce a sequence with the same elements as the ones in the nums source and is not very useful. However, there's an observable effect in this transformation: The nums and res objects are not the same. What happens is that the preceding form gets translated into the following:

```
var res = nums.Select(n => n);
```

For LINQ to Objects, the Select method is defined in the System.Linq namespace as an extension method for IEnumerable<T>:

```
public static IEnumerable<R> Select<T, R>(this IEnumerable<T> source,
    Func<T, R> projection);
```

Notice this method returns nothing more specific than an IEnumerable<R>, where R is the type parameter corresponding to the result of the projection. In this case, T and R are the same, namely int, as inferred from the identity function lambda expression. You should be able to figure this out quite easily yourself: The source is a List<int>, hence an IEnumerable<int>. Thus, T is substituted for int, and therefore the input to the projection function is an int. The project function simply returns its input, which should be an int because of that. Because the output is typed as R, we find that R is also substituted for int. Our query is turned into the following:

```
var res = Enumerable.Select<int, int>(nums, delegate (int n) { return n; });
```

Here we've used the knowledge that Select is defined as an extension method using the static Enumerable class in System.Linq.

As a result, the input, which was a List<int>, became an IEnumerable<int> that hides the original source. Therefore, it's fine to hand out the result to any read-only consumer without running the risk they cast it back to List<int> and manipulate the elements:

```
var evil = (List<int>)res; // this fails at runtime
evil.Add(0xBAD);
```

The way the original source is hidden by the Select method is something that will become clear when we discuss iterators in Chapter 20, which act as the fuel for LINQ to Objects.

## DIFFERENT LANGUAGES, SAME BEHAVIORS

The C# compiler doesn't "compile away" identity projections if the query doesn't consist of anything but that (a "degenerate query expression"):
var res = from n in nums
select n;

```
var res = from n in nums
select n;
```

The preceding will compile into a Select call that seems useless because it doesn't do anything useful, but the source-hiding property that was explained earlier is deemed important. The requirement for the user to write a select clause reflects this more or less. In Visual Basic, you can omit the Select clause if it's trivial, but to maintain the source-hiding property, the compiler will inject the identity projection Select call:

```
Dim res = From n In nums
```

If there's more than only a trivial select clause (for example, a filter preceding it), a trivial select clause is compiled away, though. The reason is that the preceding operators, like a where clause, already cause the source to get hidden:

```
var res = from n in nums
    where n % 2 == 0
    select n;
```

In C#, the user is still required to write the select clause, but this time it gets dropped at compile time, resulting in the following code:

```
var res = nums.Where(n => n % 2 == 0);
```

This illustrates how syntactical differences across C# and Visual Basic maintain the (subtle) desired behavior of trivial projections when needed.

Stand-alone identity projections are not very useful other than for their source-hiding properties. But because C# requires you to write a select clause (or a group by clause) to terminate a query expression, you'll encounter identity projections quite often:

```
var res = from n in nums
    where n % 2 == 0
    select n;
```

## Nontrivial Projections

Of more interest are the nontrivial projections that really transform elements from the input sequences into some result, possibly of another type. A simple example is shown here:

```
var twice = from n in nums
    select n * 2;
```

The output of this query is an IEnumerable<int> whose produced elements contain the original elements each multiplied by two. Internally, this translates into a Select method call, as shown before, that looks like this:

```
var twice = nums.Select(n => n * 2);
```

In other words, Select takes in a function to execute on all the source's elements, giving back the output objects. The syntactical translation carried out by the compiler for a select clause is shown in Figure 19.12. We'll ignore the case where multiple range identifiers are “in scope” for the time being.
