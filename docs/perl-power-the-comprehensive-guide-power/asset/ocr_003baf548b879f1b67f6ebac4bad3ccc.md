# # CHAPTER 8 Hashes

The assignment operations shown at comment #4 involve both the `keys()` and `values()` functions. You access and assign the keys and values in the hash to two arrays (`@ElementsAW` and `@ElementNames`).

At comment #5 you employ two `foreach` control statements. The outer `foreach` statement allows you to iterate through the `@ ElementNames` array on the basis of the keys (names of elements) it contains. When you iterate through this array, you assign each element name temporarily to a scalar, `$EName`.

The inner `foreach` statement allows you to iterate through all the values (atomic weights) in the `@ElementsAW` array. When you iterate through the `@ElementsAW` array, you assign each atomic weight temporarily to a second scalar, `$AtomicWeight`.

Given that you now have the name of the element (assigned to `$EName`) you can set up an `if` selection statement that involves supplying the name to the lookup hash operation. For each atomic weight you retrieve from the `@ElementsAW` array in the inner loop, you use the `if` statement to evaluate whether it equals the atomic weight the lookup returns. If the two are equal, then you have identified a key-value pair (`$EName` and `$AtomicWeight`). As Figure 8.6 illustrates, these you print in formatted columns.

# ## Figure 8.6

If you employ a selection statement, you can use the `values()` function to retrieve key-value pairs.

![](bbox=[0.371, 0.477, 0.841, 0.677])

# # Using the pop() Function

The `pop()` function applies to arrays, but when you pop items from an array, you diminish the size of the data container you are dealing with. If you are dealing with large collections of data, for this reason the `pop()` function offers a way to increase the performance of your program.

You can employ the `pop()` function in conjunction with an array of keys you create using the `keys()` hash function. As Listing08_06 shows, you can employ the `sort()` and `reverse()` functions so that you can alphabetize key-value pairs as you access them. The `reverse()`

192

***

TEAM LinG