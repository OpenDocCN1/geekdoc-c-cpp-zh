It is technically possible to evaluate something other than a counter variable in a for loop’s test condition, but it is certainly not typical. It is also possible to omit one (or even all) of the expressions in the for loop. In such situations, however, you should consider using the while loop.

# The while Loop

Like the for loop, while is a pretest loop. The syntax is similar, but while loops take only one expression:

```
while(condition)
    statement(s);
```

Unlike the for loop, the while loop is most often used to repeat a statement or a block of statements for a number of times that is not known before the loop begins. Usually, a statement inside the while loop’s body will set a Boolean flag to false on a certain iteration, triggering the end of the loop, as in the following example:

```
bool condition = false;
while (!condition)
{
    // This loop spins until the condition is true.
    DoSomeWork();
    condition = CheckCondition();  // assume CheckCondition()
returns a bool
}
```

# The do...while Loop

The do...while loop is the post-test version of the while loop. This means that the loop’s test condition is evaluated after the body of the loop has been executed. Consequently, do...while loops are useful for situations in which a block of statements must be executed at least one time, as in this example:

```
bool condition;
do
{
    // This loop will at least execute once, even if Condition is false.
    MustBeCalledAtLeastOnce();
    condition = CheckCondition();
} while (condition);
```

# The foreach Loop

The foreach loop enables you to iterate through each item in a collection. For now, don’t worry about exactly what a collection is (it is explained fully in Chapter 11, “Collections”); just understand that it is an object that represents a list of objects. Technically, for an object to count as a collection, it must support an interface called IEnumerable. Examples of collections include C# arrays, the collection classes in the System.Collections namespaces, and user-defined collection classes. You can get an idea of the syntax of foreach from the following code, if