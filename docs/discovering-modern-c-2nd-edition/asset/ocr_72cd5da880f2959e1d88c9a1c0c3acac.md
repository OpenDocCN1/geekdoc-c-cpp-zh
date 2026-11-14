So, he checked for everything that can go wrong and informed the caller with the appropriate error code. This is fine when the caller evaluated the error and reacted appropriately. But what happens when the caller simply ignores his return code? Nothing! The program keeps going and might crash later on absurd data, or even worse might produce nonsensical results that careless people might use to build cars or planes. Of course, car and plane builders are not that careless, but in more realistic software even careful people cannot have an eye on each tiny detail.

Nonetheless, bringing this reasoning across to programming dinosaurs like Herbert might not convince them: “Not only are you dumb enough to pass in a nonexisting file to my perfectly implemented function, then you do not even check the return code. You do everything wrong, not me.” C++17 We get a little bit more security with C++17. It introduces the attribute [[nodiscard]] to state that the return value should not be discarded: Click here to view code image

```
[[nodiscard]] int read_matrix_file(const char* fname, matrix& A)
```

As a consequence, each call that ignores the return value will cause a warning, and with an additional compiler flag we can turn each warning into an error. Conversely, we can also suppress this warning with another compiler flag. Thus, the attribute doesn’t guarantee us that the return code is used. Furthermore, merely storing the return value into a variable already counts as usage, regardless of whether we touch this variable ever again.

Another disadvantage of the error codes is that we cannot return our computational results and have to pass them as reference arguments. This prevents us from building expressions with the result. The other way around is to return the result and pass the error code as a (referred) function argument, which is not much less cumbersome. So much for messing around with error codes. Let us now see how exceptions work.

# 1.6.2.2 Throwing

The better approach to deal with problems is to throw an exception: Click here to view code image