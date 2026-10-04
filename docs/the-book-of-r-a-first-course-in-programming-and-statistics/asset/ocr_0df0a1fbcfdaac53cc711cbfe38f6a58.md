```
R> x = x + 1  # this overwrites the previous value of x
R> x
[1] -4

R> mynumber = 45.2

R> y <- mynumber*x
R> y
[1] -180.8

R> ls()
[1] "mynumber" "x"        "y"
```

As you can see from these examples, R will display the value assigned to an object when you enter the name of the object into the console. When you use the object in subsequent operations, R will substitute the value you assigned to it. Finally, if you use the ls command (which you saw in Section 1.3.1) to examine the contents of the current workspace, it will reveal the names of the objects in alphabetical order (along with any other previously created items).

Although = and <- do the same thing, it is wise (for the neatness of code if nothing else) to be consistent. Many users choose to stick with the <-, however, because of the potential for confusion in using the = (for example, I clearly didn’t mean that x is mathematically equal to x + 1 earlier). In this book, I’ll do the same and reserve = for setting function arguments, which begins in Section 2.3.2. So far you’ve used only numeric values, but note that the procedure for assignment is universal for all types and classes of objects, which you’ll examine in the coming chapters.

Objects can be named almost anything as long as the name begins with a letter (in other words, not a number), avoids symbols (though underscores and periods are fine), and avoids the handful of “reserved” words such as those used for defining special values (see Section 6.1) or for controlling code flow (see Chapter 10). You can find a useful summary of these naming rules in Section 9.1.2.

# Exercise 2.2

+   a. Create an object that stores the value 3² × 4¹/⁸.
b. Overwrite your object in (a) by itself divided by 2.33. Print the result to the console.
c. Create a new object with the value −8.2 × 10⁻¹³.
d. Print directly to the console the result of multiplying (b) by (c).