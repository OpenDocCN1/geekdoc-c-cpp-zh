+   - **Method Syntax:** Utilizes extension methods and lambda expressions, offering a more concise and flexible approach.

Both syntaxes are interchangeable, and the choice often comes down to personal preference or the specific scenario.

# Core LINQ Query Operators

LINQ provides a rich set of query operators, enabling you to perform a wide range of data manipulation tasks. Let's explore some of the most common ones:

+   - **Where()**: Filters a sequence of elements based on a specified condition.
+   - **Select()**: Projects each element of a sequence into a new form.
+   - **OrderBy() and OrderByDescending()**: Sorts a sequence of elements in ascending or descending order.
+   - **GroupBy()**: Groups elements based on a specified key.
+   - **Join()**: Combines elements from two sequences based on a matching condition.
+   - **Count(), Sum(), Average(), Min(), Max()**: Perform aggregate operations on a sequence.
+   - **FirstOrDefault(), LastOrDefault(), SingleOrDefault()**: Retrieve the first, last, or single element that satisfies a condition, or a default value if no such element exists.
+   - **Any(), All()**: Determine whether any or all elements in a sequence satisfy a condition.
+   - **Contains()**: Checks if a sequence contains a specific element.

# Practical LINQ Examples

Let's see LINQ in action with a few examples:

# 1. Filtering and Projecting Data

```
```csharp
int[] numbers = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
var evenNumbers = from num in numbers
```
```