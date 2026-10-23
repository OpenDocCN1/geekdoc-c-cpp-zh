implications as well. Java is not as object-oriented as Scala. The instances of the basic types in Java are not objects. They are called primitives and they do not have any methods. This is why their types start with lowercase letters. String is a class and instances of String are objects.

The for loop should stand out as another significant difference. The for loop in Scala is technically a for-each loop that runs through the contents of a collection. Java’s basic for loop is more of a dressed up while loop. In the parentheses there are three parts, separated by semicolons. The first part is an initializer where you set things up. This happens once, right when the loop is reached. If variables are declared there, as is the case in this example, that variable has a scope only through the loop.

The second part is a condition, just like what you would put in a while loop. It is pre-check and the loop will iterate until the condition is false. This is why the Java for loop can be described as a dressed-up while loop. The way in which the end case is determined is just like a while loop. The dressing is what comes before and after the semicolons around the condition.

The last part of what appears in the parentheses of a for loop is an iterator. This code happens after the body of the loop is evaluated and before the next condition check. In this case, the expression is ++i. This is a pre-increment of the variable i. The ++ operator in Java does an increment by 1. It can be placed before or after the variable. When it is before, the result of that expression is the incremented value. When placed after the expression the result is the value before the increment.

There is another type of for loop in Java which functions as a for-each loop. The syntax is for(type name : iterable), where type is the type in the collection, name is the variable name you want, and iterable is an object of type Iterable.

One last thing to note about the for loop is that it is never an expression. It never gives back a value. There is no equivalent to yield. The while loop in Java looks just like what you are used to in Scala.

The isPrime method also uses the return keyword. This is a valid usage in Scala, but you typically do not need it because every block is an expression with a value equal to that of the last statement in the block. In Java, blocks are not expressions, so every method that returns a value needs to specifically include a return statement at the end. If a return statement is reached inside the method, it will terminate the execution of that method and immediately jump back out to where it was called from.

The main method demonstrates Java’s array syntax. The primes variable has the type int[]. You can see the array itself is built using the new syntax. Inside of the while loop you can see that the indexing of the array is also done using square brackets, passing in the index you want to access. Arrays in Java are objects, so you can ask them how long they are using length. Note that length here is a data member. You know this in Java because there are no parentheses after it. The length of a String, however, is gotten with a method and must always have empty parentheses after it.

# A.3 File Names and Interfaces

To illustrate a few more features of Java we will use another favorite example, the bank account. We begin by introducing a supertype for bank accounts.

```
package javacode;
```