loop, you print the food group number and then proceed to print the names of the food items included in the group. To print the name of the items, you first retrieve the reference from `@ArrayInSub`. To accomplish this, you use the scalar version of the array and the current value of `$Itr` to access the index of the reference and then assign the reference temporarily to a scalar identifier (`$Ref`).

You then dereference `$Ref` and make it the target of the `foreach` repetition statement. You assign the food names that the dereferenced array (`@$Ref`) contains to the `$Name` identifier and then call the `printf()` function to print it. With each iteration of the `for` loop, you access a new reference, and given the work of the `foreach` traversal of the names, you print the contents of the three arrays. That you print them in an order that is the reverse of their position in the argument array serves only to show that you can access references to arrays and readily manipulate them.

![](bbox=[0.153, 0.381, 0.621, 0.605])

![](bbox=[0.724, 0.387, 0.933, 0.468])

# References to Functions

You can make use of the fact that every set of function blocks is in essence a reference. To create a reference to a function, you need only assign the nameless address of the function to a scalar. Here is an example of how this works:

```
```perl
$addFoods = sub{
    return join(" ", @_);
};
```
```

In this example, you assign the nameless function sub to the `$addSub` identifier. Given this bit of preparation, you can then call the function. To call a function using a reference, you have two options: