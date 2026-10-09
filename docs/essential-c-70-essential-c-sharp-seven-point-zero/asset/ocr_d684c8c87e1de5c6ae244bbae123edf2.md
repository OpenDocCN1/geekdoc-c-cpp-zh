```
{
unchecked
{
// int.MaxValue equals 2147483647
int n = int.MaxValue;
n = n + 1 ;
System.Console.WriteLine(n);
}
}
```

The results of Listing 11.9 appear in Output 11.3.

# OUTPUT 11.3

-2147483648

Even if the checked option is on during compilation, the unchecked keyword in the code in Listing 11.9 will prevent the runtime from throwing an exception during execution.

Equivalent checked and unchecked expressions are available for cases where statements are not allowed. For example, a field initializer may consist of an expression rather than a statement:

```
int _Number = unchecked(int.MaxValue + 1);
```

# SUMMARY

Throwing an exception causes a significant performance hit. A single exception causes lots of runtime stack information to be loaded and processed—data that would not otherwise be loaded—and it takes a considerable amount of time to handle. As pointed out in Chapter 5, you should use exceptions only to handle exceptional circumstances; APIs should provide mechanisms to check whether an exception will be thrown instead of forcing a particular API to be called to determine whether an exception will be thrown.

The next chapter introduces generics—a C# 2.0 feature that significantly enhances code written in C# 1.0. In fact, it essentially deprecates any use of the System.Collections namespace, which was formerly used in nearly every project.