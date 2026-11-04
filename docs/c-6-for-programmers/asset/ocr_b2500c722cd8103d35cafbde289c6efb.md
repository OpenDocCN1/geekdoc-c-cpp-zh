multiplies its two arguments. Because we’re producing a product, we begin with the value 1 in this case. Evaluation of the reduction proceeds as follows:

+   - On the first call to the lambda, parameter x’s value is Aggregate’s first argument (1) and parameter y’s value is the *first int* in values (3), producing the value 3 (1 * 3).
+   - On the next call to the lambda, parameter x’s value is the result of the first calculation (3) and parameter y’s value is the *second int* in values (10), producing the sum 30 (3 * 10).
+   - On the next call to the lambda, parameter x’s value is the result of the previous calculation (30) and parameter y’s value is the *third int* in values (6), producing the sum 180 (30 * 6).

This process continues producing a running product of the elements until they’ve all been used, at which point the final product is returned. Note again that *no mutable variables* are used to reduce the collection to the product of its elements and that the original values collection is *not* modified.

# ### 19.11.3 The Where Extension Method for Filtering Operations

Lines 38–40 *filter* the even integers in `values`, *sort* them in ascending order and display the results. You *filter* elements to produce a *new collection* of results that match a condition known as a *predicate*. LINQ extension method `Where` (line 38) receives as its argument a `Func` delegate for a method that receives one argument and returns a `bool` indicating whether a given element should be included in the collection returned by `Where`.

The lambda in line 38:

```
```csharp
value => value % 2 == 0
```
```

receives a value and returns a `bool` indicating whether the value satisfies the *predicate*—in this case, if the value it receives is divisible by 2.

# #### Sorting the Results

The `OrderBy` extension method receives as its argument a `Func` delegate representing a method that receives one parameter and returns a value that’s used to order the results. In this case (line 39), the lambda expression

```
```csharp
value => value
```
```

simply returns its argument, which `OrderBy` uses to sort the values in ascending order—for descending order you’d use `OrderByDescending`. Note again that *no mutable variables* are used to filter or sort the collection and that the original `values` collection is *not* modified.

# #### Deferred Execution

Calls to `Where` and `OrderBy` use the same *deferred execution* we discussed in Section 9.5.2—they aren’t evaluated until you iterate over the results. In lines 38–40 (Fig. 19.8), this occurs when our `Display` extension method is called (line 40). This means we can save the operation into a variable for future execution, as in

```
```csharp
var evenIntegers =
    values.Where(value => value % 2 == 0) // find even integers
          .OrderBy(value => value); // sort remaining values
```
```