| Interface | Variance |
| --- | --- |
| IEnumerable<T> | T is covariant. |
| IEnumerator<T> | T is covariant. |
| IQueryable<T> | T is covariant. |
| IGrouping<TKey, TElement> | TKey and TElement are covariant. |
| IComparer<T> | T is contravariant. |
| IEqualityComparer<T> | T is contravariant. |
| IComparable<T> | T is contravariant. |

# **Try It Yourself**

# ## Exploring Variance

By following these steps, you explore how variance works by modifying the code shown in Listing 11.12.

+   1. Create a new Console application and modify the content of Program.cs to look as shown in Listing 11.12.

+   2. Run the application using Ctrl+F5, and observe that the output matches what is shown in Figure 11.3.

![](bbox=[0.25, 0.565, 0.66, 0.66])

**FIGURE 11.3**
Printing the contents of an array

+   3. Change `PrintCollection<T>` so that it is no longer a generic method and that the type of collection is `IEnumerable<object>`.

+   4. You should immediately see the compiler errors shown in Figure 11.4.

![](bbox=[0.25, 0.754, 0.66, 0.86])

**FIGURE 11.4**
Compiler errors

+   5. Correct the two errors by commenting out the invalid lines of code. Remember, variance doesn’t work for value types, which is the reason for the compiler errors.