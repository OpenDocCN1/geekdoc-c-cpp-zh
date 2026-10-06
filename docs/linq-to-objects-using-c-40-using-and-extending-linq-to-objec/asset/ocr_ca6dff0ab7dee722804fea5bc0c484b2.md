# Output 5-14

21 22 23 24 25 26 27 28 29 30

The Take operator also allows the topmost records (the first) to be returned similar to SQL SELECT TOP(n) statement. This can be to protect against extreme result set sizes or to limit the result size during development and testing to a manageable quantity. If the page size is being retrieved from user input (like the query string in a URL), then this input should be checked and limited to avoid denial of service attacks by some setting page size to an unrealistic extreme. Listing 5-26 shows a custom extension method that has safeguards to avoid paging exploitation through malicious input. In this case, this operator limits page size to 100 elements, and handles the translation of page number and page size into Skip and Take operations making repetitive code like that shown in Listing 5-25 centralized in one place. When this operator is called with the following line, the identical results shown in Output 5-14

```
var q = nums.Page(3, 10);
```

Listing 5-26 Custom paging extension method with safeguards from extreme inputs from untrusted sources

```
public static class PagingExtensions{
    public static IEnumerable<T> Page<T>(
        IEnumerable<T> source,
        int page,
        int pageSize)
    {
        const int maxPageSize = 100;

        // clip page size to maximum
        pageSize = pageSize < maxPageSize =
            pageSize : maxPageSize;

        return source
            .Skip((page - 1) * pageSize)
            .Take(pageSize);
    }
}
```