# Introduction to Programming and Problem-Solving Using Scala

+   2. Add a quiz grade.
3. Add an assignment grade.
4. Calculate average.
5. Quit("")

```
def mainGrades {
  var tests = List[Double]()
  var assignments = List[Double]()
  var quizzes = List[Double]()
  var option = 0

  do {
    printMenu
    option=readInt()
    option match {
      case 1 =>
        println("Enter a test grade.")
        tests ::= readDouble()
      case 2 =>
        println("Enter a quiz grade.")
        quizzes ::= readDouble()
      case 3 =>
        println("Enter an assignment grade.")
        assignments ::= readDouble()
      case 4 =>
        println("The average is "+courseAverage(tests,assignments,quizzes))
      case 5 =>
      case =>
        println("Unknown option. Try again.")
    } while (option != 5)
}
```

Whether you use this or the code in section 6.6 is primarily a question of style. Most developers would probably write this version by default, but that is mainly because most developers have a background in imperative programming and will tend to favor this approach for reasons of familiarity. The form using recursion would be preferred by most programmers used to functional programming. Like the while loop, the do-while loop requires mutation and is prone to the problem of forgetting to increment which leads to an infinite loop.

# 8.3 for Loop

The while loop is logically the simplest loop, but it is not the most commonly used loop in languages. In languages that provide a for loop, it is typically the most commonly used loop. The for loop in Scala is a bit different than provided in many other languages, but you will probably find that it is the one you turn to when you are putting iteration into your code.
In languages, the natural usage of the for loop is to count so we will start with