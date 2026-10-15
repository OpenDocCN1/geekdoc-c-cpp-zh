those two arguments. The body of our anonymous method then simply returns the result of adding the current value to the running total. Since our anonymous method consists of just a single statement, we don't need to actually use the return keyword, it's implied in this case. And since this syntax is really just shorthand for defining an anonymous method that contains the required parameter list and a method body that contains whatever it is you want to execute, should you need to do something involving multiple statements, you can use a standard pair of curly braces to denote the collection of statements you would like to comprise that anonymous method. Note that when using this variation, which is officially referred to as a statement lambda, the return keyword is required. This is because the code within the curly braces can be arbitrarily complex, including the use of multiple return statements, so the compiler will no longer assume which statement should result in the return value for the functional expression.

```
{
    static void Main()
    {
        var numbers = new int[] { 1, 2, 3, 4, 5 };
        var sum = numbers.Aggregate(
            0,
            (total, num) => {
                Console.WriteLine("total = {0}, num = {1}", total, num);
                return total + num;
            }
        );

        Console.WriteLine(sum);
    }
}
```

The Aggregate method shown here is actually defined in another namespace called system.linq where link is actually an acronym that stands for language integrated query. What we've looked at so far is