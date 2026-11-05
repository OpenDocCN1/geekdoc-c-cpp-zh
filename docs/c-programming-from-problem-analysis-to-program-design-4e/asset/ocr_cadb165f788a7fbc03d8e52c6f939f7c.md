The output of this code is:

2
4
6
8
10

In order to receive the same output using a for statement, you would write:

```
for (int index = 0; index < 5; index++)
    Console.WriteLine(number[index]);
```

Notice with the for statement it is necessary to declare and increment an index to reference elements in the collection. You get automatic traversal through the collection with the foreach loop.

NOTE Note the following restriction on the foreach statement: You cannot change values in the collection. The access to the elements is read-only.

Do not be alarmed if you don't totally understand Example 6-13. As mentioned previously, the foreach statement will be revisited when you learn about arrays in the next chapter. For now, recognize that the loop body is executed for every element in the array or collection. Like the other forms of looping structures, after the iteration has been completed for all the elements in the collection, control is transferred to the next statement following the foreach block.

# Using the Do...while Structure

All of the loop structures you have learned up to this point are considered pretests. The do...while is the only posttest loop structure available in C#. The general form of the do...while statement is:

```
do
{
    statement;
}
while (conditional expression);
```

With a posttest, the statements are executed once before the conditional expression is tested. When the conditional expression evaluates to true, the statement(s) are repeated. When the expression evaluates to false, control is transferred to the statement following the do...while loop expression. Notice that the loop body is always executed at least once regardless of the value of the conditional expression.