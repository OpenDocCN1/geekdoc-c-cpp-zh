
## 24.7.4 Test-Driven Development

Unit tests are a central part of an approach to development called “Test Driven Development” (TDD). This style of development is highlighted by the idea that you write tests for code before you write the actual code. In a TDD environment, a programmer who wants to write a new class would create the class and put in blank methods which have just enough code to get the class to compile. Methods that return a value are set to return default values such as null, 0, or false. No logic or data is put in.

After that, the developer writes a basic test for the class and runs the test to see that it fails. Then just enough code is added to make that test pass. Once all existing tests pass, another test is written which fails and this process is repeated until a sufficient set of tests have been written to demonstrate that the class must meet the desired requirements in order to pass them all.

While the textbook does not follow a TDD approach, there are some significant benefits to it. The main one is that it forces a developer to take small steps and verify that everything works on a regular basis. It also gives you a feeling of security when you are making changes because you are generally feeling confident that if you make a change which breaks something, it will immediately manifest as a red bar in testing. This can be important for novice programmers who often leave large sections of code in comments because they are afraid to delete them in case something goes wrong. For this reason, the literature on TDD refers to tests as giving you the “courage” to make changes.

There is a lot more to unit testing that we have not covered here. Interested readers are encouraged to look at the JUnit website or look into Scala-based testing frameworks such as ScalaCheck and ScalaTest. Full development needs more than just unit testing as well. Unit tests, by their nature, ensure that small pieces of code work alone. To feel confident in a whole application, you need to test the parts working together. This is called integration testing and it too is done on a fairly regular basis in TDD.

## 24.8 RPN Calculator

A classic example usage of a stack is the Reverse Polish Notation (RPN) calculator. In RPN mode, operations are entered after the values that they operate on. This is also called post-fix notation. The RPN representation of “2 + 3” is “2 3 +”. While this might seem like an odd way to do things, it has one very significant advantage, there is no need for parentheses to help specify order of operation. Using standard notation, also called in-fix notation, the expressions “2 + 3 * 5” and “5 * 3 + 2” are both 17 because multiplication occurs before addition, regardless of the order things are written. If you want the addition to happen first, you must specify that with parentheses, “(2 + 3) * 5”. Using post-fix notation, you can say “3 5 * 2 +” to get 17 or “2 3 + 5 *” if we want the addition to happen first so we get 25. This lack of parentheses can significantly reduce the length of complex expressions which can be appealing when working on such things.

The evaluation of a post-fix expression can be done quite easily with a stack that holds the numbers being worked with. Simply run through the expression and for each element you do one of the following. If it is a number, you push that number onto the stack. If it is an operator, you pop two elements from the stack, perform the proper operation on them, and then push the result back on the stack. At the end there should be one value on the stack which represents the final result. We could implement this basic functionality using the following object.

```scala
object RPNCalc {
  def apply(args:Seq[String]):Double = {
    val stack = new ArrayStack[Double]
    for(arg <- args; if(arg.nonEmpty)) arg match {
      case "+" => stack.push(stack.pop+stack.pop)
      case "*" => stack.push(stack.pop*stack.pop)
      case "-" => val tmp = stack.pop; stack.push(stack.pop-tmp)
      case "/" => val tmp = stack.pop; stack.push(stack.pop/tmp)
      case x => stack.push(x.toDouble)
    }
    stack.pop
  }
}
```

These arguments are passed in as a sequence that is traversed using a for loop. The subtract and divide operators are slightly different from those for addition and multiplication simply because they are not commutative, the order of their operands matters. This code also assumes that anything that is not one of the four operators is a number.

There are a few options that would be nice to add to this basic foundation. For example, it would be nice to have a few other functions beyond the standard four arithmetic operations. It would also be nice to have support for variables so that not every value has to be a literal numeric value. A final object that supports these additions is shown here.

```scala
package scalabook.util

import scalabook.adt.ArrayStack

object RPNCalc {
  def apply(args:Seq[String],vars:collection.Map[String,Double]):Double = {
    val stack = new ArrayStack[Double]
    for(arg <- args; if(arg.nonEmpty)) arg match {
      case "+" => stack.push(stack.pop+stack.pop)
      case "*" => stack.push(stack.pop*stack.pop)
      case "-" => val tmp = stack.pop; stack.push(stack.pop-tmp)
      case "/" => val tmp = stack.pop; stack.push(stack.pop/tmp)
      case "sin" => stack.push(math.sin(stack.pop))
      case "cos" => stack.push(math.cos(stack.pop))
      case "tan" => stack.push(math.tan(stack.pop))
      case "sqrt" => stack.push(math.sqrt(stack.pop))
      case v if(v(0).isLetter) => stack.push(try { vars(v) } catch { case ex => 0.0 })
      case x => stack.push(try { x.toDouble } catch { case ex => 0.0 })
    }
    stack.pop
  }
}
```

This has added the three main trigonometric functions along with a square root function. These operations pop only a single value, apply the function, and push back the result. This code also includes an extra argument of type Map[String,Double] to store variables by name. In this case, the scala.collection.Map type is used. This is a supertype to both the mutable and immutable maps. This code does not care about mutability so this provides additional flexibility. Lastly, some error handling was added so that if a value comes in that is neither a number, nor a valid variable, we push 0.0 to the stack.

Before we can proclaim that this code works, we need to test it.² Here is a possible test configuration.

```scala
package test.scalabook.util
import org.junit._
import org.junit.Assert._
import scalabook.util.RPNCalc
class TestRPNCalc {
@Test def basicOps {
assertEquals(5,RPNCalc("2 3 +".split(" "),null),0.0)
assertEquals(6,RPNCalc("2 3 *".split(" "),null),0.0)
assertEquals(3,RPNCalc("6 2 /".split(" "),null),0.0)
assertEquals(1,RPNCalc("3 2 -".split(" "),null),0.0)
}

@Test def twoOps {
assertEquals(20,RPNCalc("2 3 + 4 *".split(" "),null),0.0)
assertEquals(3,RPNCalc("2 3 * 3 -".split(" "),null),0.0)
assertEquals(5,RPNCalc("6 2 / 2 +".split(" "),null),0.0)
assertEquals(0.25,RPNCalc("3 2 - 4 /".split(" "),null),0.0)
}

@Test def vars {
val v = Map("x" -> 3.0, "y" -> 2.0)
assertEquals(20,RPNCalc("2 x + 4 *".split(" "),v),0.0)
assertEquals(3,RPNCalc("y 3 * x -".split(" "),v),0.0)
assertEquals(5,RPNCalc("6 2 / y +".split(" "),v),0.0)
assertEquals(0.25,RPNCalc("x y - 4 /".split(" "),v),0.0)
}

@Test def specials {
val v = Map("pi" -> 3.14159, "x" -> 3.0, "y" -> 2.0)
assertEquals(0,RPNCalc("pi cos 1 +".split(" "),v),1e-8)
assertEquals(math.sqrt(2)+3,RPNCalc("y sqrt x +".split(" "),v),1e-8)
assertEquals(1,RPNCalc("pi 2 / sin".split(" "),v),1e-8)
assertEquals(0.0,RPNCalc("x y y 2 / + - tan".split(" "),v),1e-8)
}
```

As with the earlier tests, these are fairly minimal. There are literally an infinite number of tests that could be run to verify the RPN calculator. This set simply picks a few different tests related to the different types of functionality the calculator is supposed to support.

True unit testing adherents would prefer that each assertEquals be split into a separate method because none depends on the results before it. This is not just a style issue either, there are valid functional benefits to that approach. JUnit will run all the test methods independently, but each test method will stop when an assert fails. So if the processing of "2 3 +" were to fail, we would not get results from the other three lines of that test as it is written now. That makes it harder to know why it failed. If "2 3 +" fails and all the other single operator calls pass, we can feel fairly confident the problem is with the handling of "+". As it is written now, we would not get that extra information. The only reason for using the format shown here is that it takes less than half as many lines to make this readable.

> ²It is worth noting that there was a bug in this code originally that was caught by these tests.
