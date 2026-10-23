
many courses that make the cut. (Hint: Use combinations to run through all the possibilities. For each possibility, you can use map and sum to get the total “score” for that option.)

- 8. Write a function that takes a Double* and returns the median value as a Double. Your solution is not expected to be efficient. This is more of a test of your ability to do logic using the methods that were presented in this chapter.⁶
- 9. Write a function that takes an Int* and returns the mode of the values. As with the previous project, the goal here is more for you to think about how to make a solution than to make an efficient solution.

There are additional exercises and projects with data files to work on posted on the book’s website.

## Chapter 8

## Loops

- 8.1 while Loop ......................................................... 181
- 8.2 do-while Loop ........................................................ 183
- 8.3 for Loop ............................................................. 184
  - 8.3.1 Range Type ....................................................... 186
  - 8.3.2 yield ............................................................. 188
  - 8.3.3 if Guards .......................................................... 188
  - 8.3.4 Multiple Generators ................................................ 189
  - 8.3.5 Patterns in for Loops .............................................. 190
  - 8.3.6 Variable Declarations .............................................. 191
- 8.4 Multidimensional Arrays ............................................... 191
- 8.5 Testing ............................................................... 195
- 8.6 Putting it Together ................................................... 198
- 8.7 End of Chapter Material ............................................... 200
  - 8.7.1 Problem-Solving Approach .......................................... 200
  - 8.7.2 Summary of Concepts ............................................... 201
  - 8.7.3 Self-Directed Study ............................................... 202
  - 8.7.4 Exercises ....................................................... 203
  - 8.7.5 Projects ....................................................... 204

We saw in chapter 6 how we could use recursion to produce an iterative behavior where something was done multiple times. We also saw in chapter 7 that we can use collections to make certain operations happen multiple times. These approaches are the primary methods used in functional languages and they often work well to provide the functionality we need in Scala. Most languages, including Scala, provide other constructs called loops that are designed specifically for creating this iterative behavior. In this chapter we will explore the loop structures present in Scala and see how we can use these in our programs. We will start by repeating some of the things that we did previously using recursion.

### 8.1 while Loop

The most basic looping construct in Scala and many other languages is the while loop. The name tells you roughly what it does. You should keep repeating something while some condition is true. The syntax of the while loop is as follows.

```
while(condition) statement
```

The condition can be any expression that evaluates to a Boolean type. The statement is very commonly a block of code, so you will typically see the while followed by curly braces.

To see an example of this, let us use a `while` loop in a function that builds a List of numbers input by the user. The `List` will end when the user enters "quit". This is exactly like the example that we did with recursion. We could not do it with the collections because we did not know in advance how many numbers there would be.

```
def readInts:List[Int] = {
    var lst=List[Int]()
    var input=readLine()
    while(input!="quit") {
      lst=input.toInt :: lst
      input=readLine()
    }
    lst
}
```

This code is distinctly imperative. We have to declare two variables with `var` to make it work. In fact, the `while` loop and its partner, the `do-while` loop that we will discuss in the next section, are only usable as statements. They are not expressions and can not be used in places that need to have a value. The fact that the `while` loop has to be used in an imperative way is somewhat implicit in the way it works. For the code inside of the `while` loop to execute, the condition must be `true` originally. In order for the loop to finish, the value of the condition has to change to `false`. This change requires the mutation of data at some point so it is impossible to use the `while` loop in a completely functional way.

Another thing to note about the `while` loop is that it is a PRE-CHECK loop. This means that the condition is checked before the body of the loop is executed. As a result, it is possible that the contents of the loop will never execute. If the condition is `false` when the loop is first reached, the body of the loop will never execute.

Let us look at another example of the `while` loop. One of our first examples of using recursion to get iteration was the factorial. We can re-write factorial using a `while` loop in the following way.

```
def factorial(n:Int):Int = {
    var product=1
    var i=1
    while (i<=n) {
      product*=i
      i+=1
    }
    product
}
```

We declare two variables named `product` and `i` at the beginning and initialize both to the value of 1. The condition on the `while` loop causes it to iterate as long as `i` is less than or equal to `n`. Inside the loop, the value `product` is multiplied by `i` and `i` is incremented by one.

The `*=` and `+=` operators are examples of assignment operators. They provide a handy shorthand for when you want to apply a mathematical operation to a value and store the result back in the original variable. You can follow any operator by an equal sign and Scala will see it as a compound operation that performs the specified operator and stores the value back. The storing of the value is a mutation operation. As such, these operators have to be used with mutable data. That either requires `var` declarations, or mutable constructs such as `Arrays`.

This function also shows another element that is common to most `while` loops and which can lead to a common form of bugs. The line `i += 1` is what we often call the iterator of the loop. It is what moves us from one case to the next in the loop. The common bug is to accidentally leave out the iterator. Consider what happens in this code if you do that. Without the line `i += 1`, the value of `i` will never change. As a result, the condition will never change either and if it is `true` to begin with, it will be `true` forever. This leads to what we call an infinite loop, a loop that never exits. This type of error is easy to put into the code with a `while` loop, because the loop does not include anything in its structure to remind you to include the iterator.

### 8.2 do-while Loop

Scala provides a second construct that is very closely related to the `while` loop. It is the `do-while` loop. The syntax for the `do-while` loop is as follows.

```
do {
    statements
} while(condition)
```

The curly braces are not technically required here either, but it is rare to see a `do-while` loop without them. Again, the statement does very much what it says that it does. It will do the statements `while` the condition is `true`.

Given how very similar this sounds to the normal `while` loop, you might wonder what the difference is. The difference is implied by the layout. The normal `while` loop checks the condition before it executes the statements in the body of the loop. The `do-while` loop checks the condition after it executes the body of the loop. As a result, the body of a `do-while` loop will always execute at least once.

The `do-while` loop is not used that often in programming. The only times it is used are in situations where the **POST-CHECK** nature of the loop is helpful and you want the contents of the loop to always happen once. A common example of this is in menu based applications where you need to read what the user wants to do and then act on it. The decision of whether or not the loop should be executed again is based on what option the user picks.

The mainGrades function from the end of the last chapter was an example of this. In that chapter we wrote the program using recursion because that was the only method we knew for making the program execute the same code repeatedly. This function can be converted over to use a `do-while` loop and the result might look like the following.

```
def mainGrades {
    var tests = List[Double]()
    var assignments = List[Double]()
    var quizzes = List[Double]()
    var option = 0

    do {
        printMenu
        option = readInt()
        option match {
            case 1 =>
```
