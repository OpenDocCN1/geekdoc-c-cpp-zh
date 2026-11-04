variable of type `NumberPredicate`. Variable `evenPredicate` can now be used as an alias for method `IsEven`. A `NumberPredicate` variable can hold a reference to any method that receives an `int` and returns a `bool`. Lines 19–20 use variable `evenPredicate` to call method `IsEven`, then display the result. The method referenced by the delegate is called using the delegate variable’s name in place of the method’s name, as in

```
```csharp
evenPredicate(4)
```
```

# ### 19.8.3 Delegate Parameters

The real power of delegates is in passing method references as arguments to methods, as we do in this example with method `FilterArray` (lines 42–59). The method takes as arguments

+   - an `int` array and
+   - a `NumberPredicate` that references a method used to filter the array elements.

The method returns a `List<int>` containing only the ints that satisfy the condition specified by the `NumberPredicate`. `FilterArray` returns a `List`, because we don’t know in advance how many elements will be included in the result.

The `foreach` statement (lines 49–56) calls the method referenced by the `NumberPredicate` delegate (line 52) once for each element of the array. If the method call returns true, the element is included in result. The `NumberPredicate` is guaranteed to return either true or false, because any method referenced by a `NumberPredicate` must return a `bool`—as specified by the definition of the `NumberPredicate` delegate type (line 9). Line 23 passes to `FilterArray` the int array (`numbers`) and the `NumberPredicate` that references the `IsEven` method (evenPredicate). `FilterArray` then calls the `NumberPredicate` delegate on each array element. Line 23 assigns the `List` returned by `FilterArray` to variable `evenNumbers` and line 26 calls method `DisplayList` (lines 71–82) to display the results.

# ### 19.8.4 Passing a Method Name Directly to a Delegate Parameter

Line 29 calls method `FilterArray` to select the odd numbers in the array. In this case, we pass the method name `IsOdd` (defined in line 65) as `FilterArray`’s second argument, rather than creating a `NumberPredicate` variable. Line 32 displays the results showing only the odd numbers. Line 35 calls method `FilterArray` to select the numbers greater than 5 in the array, using method `IsOver5` (defined in line 68) as `FilterArray`’s second argument. Line 38 displays the elements that are greater than 5.

# ## 19.9 Lambda Expressions

Lambda expressions allow you to define simple, anonymous methods—that is, methods that do not have names and that are defined where they are assigned to a delegate or passed to a delegate parameter. In many cases, working with lambda expressions can reduce the size of your code and the complexity of working with delegates. As you’ll see in later examples, lambda expressions are particularly powerful when combined with the `where` clause in LINQ queries. Figure 19.7 reimplements the example of Fig. 19.6 using lambda expressions rather than explicitly declared methods `IsEven`, `IsOdd` and `IsOver5`.