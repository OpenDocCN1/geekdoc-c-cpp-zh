# Loops 207

that. A for loop counts from 1 to 10 and prints out the values would be written as follows in Scala.

```
for (i < 1 to 10) {
  println(i)
}
```

The name i is a variable name just like you would get with a val declaration for Scala. As such, you can call it whatever you want. For counting loops it is very common to use names as i, j, and k. However, anything will work and with other variable names, it is better if your choice communicates to those reading the code to make it easier for them to understand. After the variable name is an arrow pointing to the left made of a hyphen and minus sign. You will see this in all for loops in Scala. You can read the “in”. After that is a nice expression that you should be able to read. We will talk more about exactly what this means. You can read that for loop as something like “for in 1 to 10”.

As we saw in chapter 6, the indexes in collections in Scala do not start counting at zero. As such, you would not count from 1 to 10. Instead, we would normally count from 0 up to 9. This could be expressed in Scala by replacing 1 to 0 with 10. However, it is very common to start at zero and express the number of elements you want to go through. For this reason you may use until instead of to, thus following also works in Scala.

```
for (i < 0 until 10) {
  println(i)
}
```

Using until causes the counting to finish one before the last value listed.
The for in Scala is not just counting though. Indeed, this usage is something of a special case in Scala. In general, the expression to read the <- in a for loop in Scala can evaluate any type of collection. In other languages, this type of loop runs through the elements of a collection is often called a FOR-EACH loop because it does something for each element of the collection. This might remind you of the foreach method from section 6.5. This is more than a passing resemblance.

To illustrate this usage of the for loop, consider the following code in the REPL:

```
scala> List.tabulate(10)(i => i*i)
res0: List[Int] = List(0, 1, 4, 9, 16, 25, 36, 49, 64, 81)
scala> for (elem <- res0) {
  println(elem)
}
```

+   0
1
4
9
16
25
36
49
64
81

In this case, the for loop actually does exactly the same thing that foreach does and runs the code inside the loop on each of the different elements in the list. What code you see