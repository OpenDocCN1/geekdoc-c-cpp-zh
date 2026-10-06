
# Introduction to Programming and Problem-Solving Using Scala

## Listing 3.2: TimeConvertInExpr.scala

```scala
import io.StdIn._
print("Enter the number of seconds.")
val totalSeconds = readInt()
val response = if (totalSeconds > 0) {
  val displaySeconds = totalSeconds%60
  val totalMinutes = totalSeconds/60
  val displayMinutes = totalMinutes%60
  val displayHours = totalMinutes/60
  val sec = displaySeconds.toString
  val min = displayMinutes.toString
  displayHours+":"
```

## Common Bug

One common error that novice programmers encounter with the if statement occurs when they put more than one expression after the if or the else without curly braces. This is an example of how that can happen. We start with the following code that calculates an area.

```scala
val area = if (shape=="circle")
math.Pi*radius*radius
else
length*width
```

Here it is broken across multiple lines so there is not one long line of code. This can make it easier to read. (Note that this code does not work in the REPL as it ends the expression when you hit enter before the if) There are no curly braces, but they are not needed each part of the if has only one expression.

Now consider the possibility that the program this is part does not work. To help figure out what is going on, put print statements in so that you know when it uses the case circle and when it uses the rectangle. The error comes when the code is changed to something like this.

```scala
val area = if (shape=="Circle")
println("Circle")
math.Pi*radius*radius
else
println(Rectangle)
length*width
```

Now both branches have two expressions, and we have a problem. This code needs curly braces, but they are easy to forget because the indentation makes the code fine. Scala does not care about indentation. That is only for the benefit of humans. In reality, this code should look something like the following.

```scala
val area = if (shape=="circle") {
println("Circle")
math.Pi*radius*radius
else {
println("Rectangle")
length*width
}
```

Returning to the theme park example, what about the other parts of our admission park entrance cost? We also wanted to check if the person had a cooler or if they wanted to get into the water. These should be variables of type Boolean. We might call them cooler and waterPark. Let us say it as an additional $5 to bring in a cooler and $110 to the water. If we used the park as an expression, we can type it in the following:

```scala
val cost = (if (age<13) 20 else 35)+(if (cooler) 5 else 0)+(if (waterPark) 10 else 0)
```

Here we are adding the results of three different expressions. This format is maybe specific to functional languages. It would be more common in most languages to see this:

```scala
var cost = 20
val cooler = false
val waterPark = true
if (age >= 13) cost = 35
if (cooler) cost +=5
if (waterPark) cost +=10
```

In this second form, we use if as a statement instead of an expression and have the body of the change, or mutate, the value of the variable cost.

## Note on Style

While there are differences between the functional and imperative versions of code in different applications in regards to things performance and the likelihood of errors, at this stage these should not be your top concerns. You should pick the style that makes the most sense to you. Later you can evaluate the differences and pick the approach that best fits the task.

In the second and third statements, the name cost is repeated. This type of repetition is often avoided in programming. Many languages, including Scala, include operations that allow us to avoid it. When the duplication is like this, with an assignment and a variable appearing on both sides of the equals sign, it is possible to use an abbreviated syntax where the operator is placed in front of the equals sign in the following:

```scala
var cost = 20
val cooler = false
val waterPark = true
if (age >= 13) cost = 35
if (cooler) cost += 5
if (waterPark) cost += 10
```

## Introduction to Programming and Problem-Solving Using Scala

Note that the functional and imperative versions of code in different applications in regards to things performance and the likelihood of errors, at this stage these should not be your top concerns. You should pick the style that makes the most sense to you. Later you can evaluate the differences and pick the approach that best fits the task.

## 3.3 Comparisons

The simplest comparisons are the ones that compare two values to see if they are equal or not. These are the relational operators. In Scala, these include `==`, `!=`, `>`, `<`, `>=`, and `<=`. Here are some examples of how to use them:

- `==` (equal)
- `!=` (not equal)
- `>` (greater than)
- `<` (less than)
- `>=` (greater than or equal to)
- `<=` (less than or equal to)

These operators all return a Boolean value (`true` or `false`).

```scala
val x = 5
val y = 10
x == y // false
x != y // true
x > y  // false
x < y  // true
x >= y // false
x <= y // true
```

## Equality Identity (Advanced)

In Scala, the `==` operator checks if two objects have the same value. This is known as equality. However, sometimes you might want to check if two objects are the same instance in memory. This is known as identity. To check for identity, you use the `eq` operator.

```scala
val s1 = "hello"
val s2 = "hello"
s1 == s2 // true (they have the same value)
s1 eq s2 // false (they are different objects in memory)
```

## 3.4 Boolean Logic

Imagine if the park had a policy where seniors are charged the same amount as children. Now anyone over 65 or under 13 should pay the reduced rate. We could accomplish this by separating statements in either the functional or the imperative manner.

```scala
var cost = if (age < 13 || age > 65) 20 else 35
```

This is much cleaner than the alternative. What we would really want to say is exactly what we said in English. We want to say that we use the lower rate if the
