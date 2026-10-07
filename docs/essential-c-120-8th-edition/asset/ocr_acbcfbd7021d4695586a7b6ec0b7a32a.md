# 218 Chapter 5: Parameters and Methods

Besides the basics of calling and defining methods, this chapter covers some slightly more advanced concepts—namely, recursion, method overloading, optional parameters, and named arguments. All method calls discussed so far and the end of this chapter are static (a concept that Chapter 6 explores in detail).

Even as the HelloWorld program in Chapter 1, you learned how to define a method. In that example, you defined the Main() method. In this chapter, you will learn about method creation in more detail, including the special C# syntaxes (ref and out) for parameters that pass variables rather than values to methods. Lastly, we will touch on rudimentary error handling.

# Calling a Method

> BEGINNER TIP

What Is a Method?
Up to this point, almost all of the statements in the programs you have written appeared together in a list without any grouping outside of what the statement or code block provided. When programs become any more complex, this approach quickly becomes difficult to maintain and complicated to read through and understand.

A method is a means of grouping together sequence a of statements to perform a particular action or compute a particular result. This provides greater structure and organization for the statements that compose a program. Consider, for example, a Main() method that counts the lines of source code in a directory. Instead of having one large Main() method, you can provide a shorter version that allows you to hone in the details of each method implementation as necessary. Listing 5.1 shows an example.

# LISTING 5.1: Grouping Statements into Methods

```
public class Program
{
    public static void Main()
{
        int lineCount;
    }
}
```