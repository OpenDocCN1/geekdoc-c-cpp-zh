The difference between both is the same as in Swift: if the condition is false on `while` the code block will never run, while `do`...`while` will run once.

This is similar in Swift to the `while` and `repeat-while` loop:

```
```kotlin
while condition {
    //Do something
}

repeat {
    //Something
} while condition
```
```

# Ternary operator

It doesn’t exist in Kotlin. This is something that has been under discussion for a couple of years now, and the result has always been the same: you can achieve the same solution by using an inline **if... else** condition.

# Collections

Kotlin supports different types of collections: arrays, lists and maps. These are immutable by default, but you can use their mutable counterpart by using: **mutableList** and **mutableMap**.

Although on Swift you can change the mutability of a list or a dictionary if you declare it with **let** (immutable) or **var** (mutable), the same is not valid for Kotlin. As mentioned above, you’ve got the **list** and **map** for immutable variables, and **mutableList** and **mutableMap** for mutable.

# Lists

You can easily create a list in Kotlin from a source set by calling `listOf` and add the items as parameters. You can see an example where this is done on the **MainScreen.kt** file inside the **androidApp/main** folder:

```
```kotlin
val bottomNavigationItems = listOf(
    BottomNavigationScreens.Home,
    BottomNavigationScreens.Bookmark,
    BottomNavigationScreens.Latest,
    BottomNavigationScreens.Search
)
```
```

In this case, this is the list of items in the navigation bar.

Imagine that you want to add a new item to this list. You can’t. There’s no add or