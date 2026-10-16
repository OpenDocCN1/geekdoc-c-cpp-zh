What we haven’t discussed properly yet, where variables are concerned, is scope. Variable scope is referring to points in your code where a variable is valid, where it exists. In other words, where it can be used and referred to.

Let’s say we have a method that we created. Inside that method, a variable is created, such as int aNumber = 3. We can use this variable anywhere within the method but it can’t be used inside of any other method. This variable only has scope inside the method in which it was created, nowhere else.

Here’s another example:

```
public void DoSomething()
{
    for(int x = 0; x < 10; x++)
    {
        Console.WriteLine(x);
    }

    x = -5; // This will not compile because the variable called x is not in scope.
}
```

What we have here is a for loop and inside is a variable with a name of x. That variable is only valid within the for loop. Once we exit that loop, the variable can’t be used anywhere else or at any other time.

What we can do is create another for loop and have another variable inside it, a different one also called x but neither will conflict with each another:

```
public void DoSomething()
{
    for(int x = 0; x < 10; x++)
```