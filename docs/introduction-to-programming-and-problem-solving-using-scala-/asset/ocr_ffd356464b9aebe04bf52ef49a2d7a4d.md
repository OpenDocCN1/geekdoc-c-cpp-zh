# Introduction to Programming and Problem-Solving Using Scala

+   - Variables can be replaced with their values.

+   - if-expressions are evaluated based on the value of the condition.

+   - if (true) trueExpr else falseExpr -> trueExpr
- if (false) trueExpr else falseExpr -> falseExpr

+   - A function call is replaced by the body of the function where all parameters have been substituted by the arguments in the call.

To understand these rules, we will run through a little example. One of the authors teaches a roller skating class where most of the grade comes from various skills and an endurance test. The following code can be used to calculate how many points a particular student gets from them.

# Listing 4.5: SkatingPoints.scala

```
def skillPoints(numSkills:Int):Int = 5*numSkills
def endurancePoints(numLaps:Int):Int = {
  if (numLaps < 20) 20
  else if (numLaps > 40) 20
  else numLaps-20
}
```

```
val skills = 9
val laps = 36
val points = skillPoints(skills) + endurancePoints(laps)
```

It has been broken up to use two small functions, for each component. This example also codes the values instead of using readInt because that would be a side effect which would complicate the use of substitution.

What we want to do is find the value of points by substitution. The expression we want to evaluate

```
skillPoints(skills) + endurancePoints(laps)
```

The first thing we do is to substitute in the values of the two vals. This gives us the following.

```
skillPoints(9) + endurancePoints(36)
```

Note that this is technically doing two things at once. That is to keep the discussion shorter. You should do the substitutions one at a time. If there is more than one available, you can pick which one to do first, because there are no side effects, the order does not matter. Next we will expand the call to skillPoints.

```
5*9 + endurancePoints(36)
```

Remember that this is done by replacing the call with the body of the function where parameters have been replaced by arguments. So the numSkills in skillPoints was replaced by the value 9. We can then evaluate 5*9.

```
45 + endurancePoints(36)
```