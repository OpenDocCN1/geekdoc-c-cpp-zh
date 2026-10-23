4. Write an if statement.

# 5.9.2  Summary of Concepts

+   - Functions are used to break problems up into smaller pieces.
+     - Help solve problems.
+     - Informative names make code more understandable.
+     - Smaller functions are easier to work with.
+   - The functions in programming are similar to those from math. Information is passed in through formal parameters. The value of the parameters is determined at the time the function is called when arguments are passed in.
+   - Functions are declared in Scala using `def`. This is followed by the function name, an argument list, a result type, and then an equals sign with the expression for the function. Result type can be left off and inferred, but it is recommended you include it anyway.
+   - Functions can also be written as literals in Scala.
+     - The rocket notation has argument list and body separated by `=>`.
+     - Shorter notation uses underscores for arguments. Only works for certain functions.
+   - Functions that are called only for their side effects and do not need to return a value return `Unit`. This is done enough that there is a simplified syntax where the colon, result type, and equals sign are left off and curly braces go after the argument list.
+   - If you have functions that often take or return tuples, it can be useful to use a type declaration to give shorter, meaningful names to the tuples.

# 5.9.3  Self-Directed Study

Enter the following statements into the REPL and see what they do. Some will produce errors. You should figure out why. Try some variations to make sure you understand what is going on.

```
scala> def succ(n:Int):Int = n+1
scala> succ(1)
scala> succ(succ(1))
scala> var cnt = 0
scala> def inc { cnt=cnt+1 }
scala> cnt
scala> inc
scala> cnt
scala> inc
scala> inc
scala> cnt
scala> val f = (x:Double,y:Double)=>math.sqrt(x*x+y*y)
scala> f(3,4)
scala> def doThreeTimes(g:(Double)=>Double,x:Double) = g(g(g(x)))
```