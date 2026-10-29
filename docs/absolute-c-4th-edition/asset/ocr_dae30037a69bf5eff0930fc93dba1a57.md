+   3. In the code given in Self-Test Exercise 1, what is the throw statement?
+   4. What happens when a throw statement is executed? (Tell what happens in general, not simply what happens in the code in Self-Test Exercise 1 or some other sample code.)
+   5. In the code given in Self-Test Exercise 1, what is the try block?
+   6. In the code given in Self-Test Exercise 1, what is the catch block?
+   7. In the code given in Self-Test Exercise 1, what is the catch-block parameter?

# DEFINING YOUR OWN EXCEPTION CLASSES

A throw statement can throw a value of any type. A common thing to do is to define a class whose objects can carry the precise kinds of information you want thrown to the catch block. An even more important reason for defining a specialized exception class is so that you can have a different type to identify each possible kind of exceptional situation.

An exception class is just a class. What makes it an exception class is how it is used. Still, it pays to take some care in choosing an exception class’s name and other details.

Display 18.3 contains an example of a program with a programmer-defined exception class. This is just a toy program to illustrate some C++ details about exception handling. It uses much too much machinery for such a simple task, but it is an otherwise uncluttered example of some C++ details.

Notice the throw statement, reproduced in what follows:

```
throw NoMilk(donuts);
```

The part NoMilk(donuts) is an invocation of a constructor for the class NoMilk. The constructor takes one int argument (in this case, donuts) and creates an object of the class NoMilk. That object is then thrown.

# MULTIPLE THROWS AND CATCHES

A try block can potentially throw any number of exception values, which can be of differing types. In any one execution of the try block, at most one exception will be thrown (since a throw statement ends the execution of the try block), but different types of exception values can be thrown on different occasions when the try block is executed. Each catch block can only catch values of one type, but you can catch exception values of differing types by placing more than one catch block after a try block. For example, the program in Display 18.4 has two catch blocks after its try block.

Note that there is no parameter in the catch block for DivideByZero. If you do not need a parameter, you can simply list the type with no parameter. This is discussed a bit more in the programming tip section entitled "Exception Classes Can Be Trivial."