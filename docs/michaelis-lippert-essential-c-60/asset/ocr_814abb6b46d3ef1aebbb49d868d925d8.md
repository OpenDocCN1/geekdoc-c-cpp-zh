Besides the basics of calling and defining methods, this chapter covers some slightly more advanced concepts—namely, recursion, method overloading, optional parameters, and named arguments. All method calls discussed so far and through the end of this chapter are static (a concept that Chapter 5 explores in detail).

Even as early as the HelloWorld program in Chapter 1, you learned how to define a method. In that example, you defined the Main() method. In this chapter, you will learn about method creation in more detail, including the special C# syntaxes (ref and out) for parameters that pass variables rather than values to methods. Lastly, we will touch on some rudimentary error handling.

# Calling a Method

# BEGINNER TOPIC

# What Is a Method?

Up to this point, all of the statements in the programs you have written have appeared together in one grouping called a Main() method. When programs become any more complex than those we have seen thus far, a single method implementation quickly becomes difficult to maintain and complex to read through and understand.

A method is a means of grouping together a sequence of statements to perform a particular action or compute a particular result. This provides greater structure and organization for the statements that comprise a program. Consider, for example, a Main() method that counts the lines of source code in a directory. Instead of having one large Main() method, you can provide a shorter version that allows you to hone in on the details of each method implementation as necessary. Listing 4.1 shows an example.

# LISTING 4.1: Grouping Statements into Methods

```
class LineCount
{
    static void Main()
    {
        int lineCount;
        string files;
```