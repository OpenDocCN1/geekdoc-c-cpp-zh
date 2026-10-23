because it is often hard to predict if you will need to extend something in the future. You might not feel this in courses, but it becomes very significant in professional development when you often are not told up front exactly what is wanted of you and even when you are, the customer is prone to change their mind later in the process.

# 6.5 Matching

The if expression is not the only conditional construct in Scala. There is a second, far more expressive, conditional construct, match. While the if construct picks between two different possibilities, based on whether an expression is true or false, the match construct allows you to pick from a large number of options to see if a particular expression matches any of them. The term “matches” here is vague. Indeed, the power of the match construct comes from something called PATTERN MATCHING.

The syntax of the match expression in its simplest form is as follows.

```
expr match {
  case pattern1 => expr1
  case pattern2 => expr2
  case pattern3 => expr3
  ...
}
```

The value of the expression before the match keyword is checked against each of the different patterns that follow the case keywords in order. The first pattern that matches will have its expression evaluated and that will be the value of the whole match expression.

We can use this to repeat our example from chapter 4 related to the cost of food at a theme park.

```
def foodPriceMatch(item:String,size:String):Double = item match {
  case "Drink" => size match {
    case "S" => 0.99
    case "M" => 1.29
    case _ => 1.39
  }
  case "Side" => size match {
    case "S" => 1.29
    case "M" => 1.49
    case _ => 1.59
  }
  case "Main" => size match {
    case "S" => 1.99
    case "M" => 2.59
    case _ => 2.99
  }
  case _ => size match {
    case "S" => 4.09
    case "M" => 4.29
    case _ => 5.69
  }
}
```