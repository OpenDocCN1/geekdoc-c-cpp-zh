```
if (productCategory == "Coffee")
{
    // Do something
}
else if (productCategory == "Food")
{
    // Do something
}
else
{
    // Do something else
}
```

So in this example, if the product category is coffee, the first block will execute and the blocks below it will be skipped by program flow. If the product category is not coffee, the else/if expression will be evaluated instead. If the category is food, that second block will execute and the else block at the bottom will be skipped again. However, if the product category is not coffee or food, this final else block will execute as a fallback regardless of what the category value is. Let's look at an example of how to work with these types of statements in our code project. Let's see how we can start to use