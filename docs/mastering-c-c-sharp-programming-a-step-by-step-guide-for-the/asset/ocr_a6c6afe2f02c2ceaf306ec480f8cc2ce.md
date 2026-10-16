Because an anonymous method has no name, it is an easy way to create instances of delegates without the need to write a separate function or method as you can see from the brief example above. Using an anonymous method, we could rewrite the first part of that example like this:

```
delegate (Employee emp)
{
    Return emp.ID == 02;
}
```

As you can see, we have replaced the FindEmp() function from the first example with a delegate.

# Lambda Expressions

As with the anonymous methods, it is better to write the blocks of code inline and this requires the use of delegates. Here’s an example:

```
int res = list.Find(delegate(int n)
{
    if (n == 5) return true;
    else return false;
});
```

You can see from this example that writing the syntax for the anonymous method is a little bit harder and isn’t all that easy to manage.

In v3.0 of C#, we saw the lambda expression. This gives us a much easier and more concise syntax, more functional and better to use to write those anonymous methods.

Lambda expressions are written as lists of parameters, with the lambda operator (=>) following the list. After this is an expression or a block of statements. Here’s an example of a lambda expression: