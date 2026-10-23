```
```
val another = readLine()
if(another=="Y") {
  val (people, cost) = groupSizeCost()
  val (morePeople, moreGroups, moreCost) = doAdmission()
  (people+morePeople, 1+moreGroups, cost+moreCost)
} else (0,0,0.0)
}

val (totalPeople, totalGroups, totalCost) = doAdmission()
println("There were "+totalPeople+" people in "+totalGroups+
    " groups who paid a total of "+totalCost)
```
```

This code has two different recursive functions, one for groups and one for people. The `doAdmission` function recurses over full groups. It asks each time if there is another group and if there is it uses `groupSizeCost` to get the number of people and total cost for the next group, then adds those values to the return of the recursive call. The `groupSizeCost` function uses the recursive `individualAdding` function to run through the proper number of people, ask their age, and add them all up.

One interesting point to notice about `individualAdding` is that the function takes a `Boolean` for whether or not there is a cooler, but when it recursively calls itself, it always passes `false` for that argument. This is a simple way to enforce our rule that each group only brings in one cooler. If the initial call uses `true` for cooler, that will be used for the first person. All following calls will use a value of `false`, regardless of the value for the initial call.

# ## Bad Input, Exceptions, and the try/catch Expression

At this point, you have probably noticed that if you call `readInt` and enter something that is not a valid `Int` it causes the program to crash. If you looked closely at the output when that happens you have noticed that it starts with `java.lang.NumberFormatException`. This is the error type reported when the program is expecting a number and gets something that does not fit that requirement. The `NumberFormatException` is just one type of `Exception`. There are many others and we will learn in section 22.3 that you can make your own.

For the first half of this book we generally assume that users will input appropriate values. As such, we do not include code for handling situations when they do not. If you want to be able to make more flexible code or simply deal nicely with users giving invalid inputs you need to use the `try/catch` expression. This begins with a `try` block that does what the name implies, it is going to try to execute a piece of code with the knowledge that it might fail. This is followed by a `catch` block with different cases for things that could go wrong. Here is a very basic example where we try to read an integer and give back the value that is read if it works, otherwise it gives us zero.

```
```
val num = try {
  readInt()
} catch {
  case _ => 0
}
```
```

As this shows, the `try/catch` is an expression with a value. One point to keep in mind