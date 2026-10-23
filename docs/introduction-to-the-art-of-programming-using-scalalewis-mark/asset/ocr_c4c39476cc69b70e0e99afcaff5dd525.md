```
scala> val min="5"
min: java.lang.String = 5

scala> val sec="2"
sec: java.lang.String = 2

scala> val finalString=displayHours+":"+("0"*(2-min.length))+min+":"+(
| "0"*(2-sec.length))+sec
finalString: java.lang.String = 34:05:02
```

# 3.8 Sequential Execution

Working in the REPL is great for certain tasks, but what if you have a sequence of things you want to do, and you want to do it multiple times. Having to type in the same set of instructions repeatedly is not a very good option. What we just did is a perfect example of that. If we want to do this for a different number of seconds, we have to repeat all the commands we just performed. Indeed, you can not really say that you have programmed until you put in a fixed set of instructions for solving a problem that you can easily run multiple times. That is what a program really is. So now it is time to write our first program of any significance.

We have used the REPL to enter commands one at a time. This is a great way to test things out in Scala and see what a few commands do. A second way of giving commands to Scala is to write little programs as SCRIPTS. The term script is used to describe small programs that perform specific tasks. There are languages, called scripting languages, that have been created specifically to make the task of writing such small programs easier. Scala is not technically a scripting language, but it can be used in that way. The syntax was created to mirror a lot of the things that are commonly put into scripting languages and if you run the scala command and give it the name of a file that ends in .scala, that file will be run as a script where the statements in it are executed in order.⁴ We will use Scala as a scripting language until chapter 17 when we move up to a different style that helps us to organize larger pieces of code. The script for our time conversion looks like this.

```
val totalSeconds=123456
val displaySeconds=totalSeconds%60
val totalMinutes=totalSeconds/60
val displayMinutes=totalMinutes%60
val displayHours=totalMinutes/60
val sec=displaySeconds.toString
val min=displayMinutes.toString
val finalString=displayHours+":"+("0"*(2-min.length))+min+
":"+("0"*(2-sec.length))+sec
println(finalString)
```

If you put this into a file called TimeScript.scala and then run scala TimeScript.scala, you will get the output 34:17:36. The println statement is required for the script because

> ⁴We will see later that the statements are not always executed in order because there are statements that alter the flow of control through the program. Since we have not gotten to those yet though, execution is completely sequential at this point.