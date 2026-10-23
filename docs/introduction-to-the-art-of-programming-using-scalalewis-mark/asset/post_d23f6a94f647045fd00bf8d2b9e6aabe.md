
implications as well. Java is not as object-oriented as Scala. The instances of the basic types in Java are not objects. They are called primitives and they do not have any methods. This is why their types start with lowercase letters. String is a class and instances of String are objects.

The for loop should stand out as another significant difference. The for loop in Scala is technically a for-each loop that runs through the contents of a collection. Java’s basic for loop is more of a dressed up while loop. In the parentheses there are three parts, separated by semicolons. The first part is an initializer where you set things up. This happens once, right when the loop is reached. If variables are declared there, as is the case in this example, that variable has a scope only through the loop.

The second part is a condition, just like what you would put in a while loop. It is pre-check and the loop will iterate until the condition is false. This is why the Java for loop can be described as a dressed-up while loop. The way in which the end case is determined is just like a while loop. The dressing is what comes before and after the semicolons around the condition.

The last part of what appears in the parentheses of a for loop is an iterator. This code happens after the body of the loop is evaluated and before the next condition check. In this case, the expression is ++i. This is a pre-increment of the variable i. The ++ operator in Java does an increment by 1. It can be placed before or after the variable. When it is before, the result of that expression is the incremented value. When placed after the expression the result is the value before the increment.

There is another type of for loop in Java which functions as a for-each loop. The syntax is for(type name : iterable), where type is the type in the collection, name is the variable name you want, and iterable is an object of type Iterable.

One last thing to note about the for loop is that it is never an expression. It never gives back a value. There is no equivalent to yield. The while loop in Java looks just like what you are used to in Scala.

The isPrime method also uses the return keyword. This is a valid usage in Scala, but you typically do not need it because every block is an expression with a value equal to that of the last statement in the block. In Java, blocks are not expressions, so every method that returns a value needs to specifically include a return statement at the end. If a return statement is reached inside the method, it will terminate the execution of that method and immediately jump back out to where it was called from.

The main method demonstrates Java’s array syntax. The primes variable has the type int[]. You can see the array itself is built using the new syntax. Inside of the while loop you can see that the indexing of the array is also done using square brackets, passing in the index you want to access. Arrays in Java are objects, so you can ask them how long they are using length. Note that length here is a data member. You know this in Java because there are no parentheses after it. The length of a String, however, is gotten with a method and must always have empty parentheses after it.

## A.3 File Names and Interfaces

To illustrate a few more features of Java we will use another favorite example, the bank account. We begin by introducing a supertype for bank accounts.

```
package javacode;
```

There are many things in this class that are worth noticing. Before looking at the details though, we should note something that is not at all obvious here. The BankAccount interface is located in a file called "BankAccount.java". The CheckingAccount class is in a separate file called "CheckingAccount.java". In Scala it was recommended that separate class, trait, and object declarations be put in separate files with names that match. In Java, this is not just recommended, it is required. There can be only one top-level public declaration per file in Java, and its name must match the name of the file.

So what are some of the differences between this code and what you would have written in Scala? For one thing, the name member is preceded by the final keyword. In Scala, final means that something can not be overridden in a subtype. When applied to a method, it has that same meaning in Java. However, when used in front of a variable declaration, it means that the value of that variable can not be changed after it is set. A final variable in Java is like a val declaration in Scala. Without final, it is like you are using var.

There is something else worth noting about name, it is not given a value. In Scala, any member without a value is considered abstract. This is not the case in Java. You can declare variables either locally or as class members without providing an initial value. For local variables, Java will check that they are not used before initialization and give you an error if that happens. For member variables there is no error. Instead, they are given a default value. For primitives the default is 0, 0.0, or false, depending on the exact type. For object types, typically called reference types in Java, they are given the value of null. This is a very common source of errors in Java and that is one of the reasons Scala forces you to initialize variables.

## A.4 Constructors and @Override

With this example it also starts to become obvious that there are no arguments to the class. Argument lists are not required for Scala, but in this situation they would clearly have been useful. There are no argument lists for classes in Java. To get information into an object when it is instantiated in Java, you write CONSTRUCTORS. A constructor is a method that gets called when an object is instantiated. By default, Java creates a constructor that takes no arguments. If you include any constructor of your own, the default one is no longer created for you. A constructor looks like a method except that it has no return type, not even void, and the name matches the name of the class. In CheckingAccount you can see that there is a constructor directly after the two lines declaring the member data. This constructor takes initial values for the member data and sets it.

There are some things worth noting here. First, writing a little class in Java with member data that can be set at construction is much more verbose in Java than it is in Scala. The class needs to contain declarations of the data members and a constructor that sets them instead of just listing them with val or var in an argument list. One could argue that the payoff of this is that the syntax for multiple constructors is a bit cleaner.

After the constructor are the two methods required by the supertype along with two others for doing deposits and withdraws. These should all be fairly straightforward at this point. The only thing really new is the @Override annotation. Scala made override a keyword in the language. Java did not do that originally, but added the annotation in later. This is not required in Java, but for the same reasons it is required in Scala, it is strongly

## A.5 Generics and Polymorphism

To make the accounts useful, they need to be put into a bank. This is something that could involve a large amount of code, but we will stick to a very short example to demonstrate the basic concepts. Here is simple Bank class that keeps track of accounts using a Java collection.

```
package javacode;

import java.util.*;

public class Bank {
    private List<BankAccount> accounts = new ArrayList<BankAccount>();

    public void makeNewCheckingAccount(Scanner sc) {
        System.out.println("Who is the new checking account for?");
        String name = sc.next();
        System.out.println("What is the starting balance in cents?");
        int bal = sc.nextInt();
        accounts.add(new CheckingAccount(name,bal));
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Bank bank = new Bank();
        bank.makeNewCheckingAccount(sc);
        for (BankAccount ba:bank.accounts) {
            System.out.println(ba.getName()+" "+ba.getBalance());
        }
    }
}
```

The accounts are specifically stored in a java.util.List. The closest equivalent to this in Scala is the mutable.Buffer. Like the Buffer, the List is implemented using both an array and a linked list. You can see here that we have gone with the array-based implementation.

The fact that Java used square brackets for arrays means that something else must be used for type parameters. These are called GENERICS in Java and they are put inside of angle braces, the characters we typically read as less than and greater than. As with Scala, you can make Java classes or methods generic. The generic type is typically inferred for methods, but not for classes.

If you want to make a collection or just a reference that can hold “anything” in Java, the common supertype is Object. Technically, Object is equivalent to AnyRef. The fact that primitives are not objects means they are not instances of any class. They are not involved in supertype/subtype relationships. To get around this, Java includes wrapper types like java.lang.Integer and does something called autoboxing to wrap up primitives in a way
