
A run of the code in Listing 18-2 is shown in Figure 18-2. The code stores Barry A. Burd in a variable called fullName and displays the fullName variable's content as part of the output. To make this program work, you have to store Barry A. Burd somewhere. After all, the program follows a certain outline:

```
Get a name.
Get some other stuff.
Compute the total.
Display the name (along with some other stuff).
```

![](img/bf4858233d2b2a32ff4e3991860526b3_365_0.png)

Figure 18-2
Making a purchase.

If you don't have the program store the name somewhere, by the time it's done getting other stuff and computing the total, it forgets the name (so the program can't display the name).

## Reading and writing strings

To read a String value from the keyboard, you can call either next or nextLine:

The method next reads up to the next blank space.
For example, with the input Barry A. Burd, the statements

```
String firstName = keyboard.next();
String middleInit = keyboard.next();
String lastName = keyboard.next();
```

assign Barry to firstName, A. to middleInit, and Burd to lastName.

The method nextLine reads up to the end of the current line.
For example, with input Barry A. Burd, the statement

```
String fullName = keyboard.nextLine();
```

assigns Barry A. Burd to the variable fullName. (Hey, being an author has some hidden perks.)

### Listing 18-4: An Attempt to Debug the Code in Listing 18-3

```java
import java.util.Scanner;
import static java.lang.System.out;

class DebugCheckPassword {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        String password = "swordfish";
        String userInput;

        out.print("What's the password? ");
        userInput = keyboard.next();

        out.println();
        out.println("You typed           ");
        out.println(userInput);
        out.print("But the password is ");
        out.println(password);
        out.println();

        if (password == userInput) {
            out.println("You're okay!");
        } else {
            out.println("You're a menace.");
        }

        keyboard.close();
    }
}
```

### Figure 18-4
This looks even worse.

![](img/bf4858233d2b2a32ff4e3991860526b3_368_0.png)

Ouch! I'm stumped this time. The run in Figure 18-4 shows that both the userInput and password variables have value swordfish. So why doesn't the program accept the user's input?

When you compare two things with a double equal sign, reference types and primitive types don't behave the same way. Consider, for example, int versus String:

You can compare two int values with a double equal sign. When you do, things work exactly as you would expect. For example, the condition in the following code is true:

```
int apples = 7;
int oranges = 7;

if (apples == oranges) {
    System.out.println("They're equal.");
}
```

When you compare two String values with the double equal sign, things don't work the way you expect. The computer doesn't check to see if the two String values contain the same letters. Instead, the computer checks some esoteric property of the way variables are stored in memory.

![](img/bf4858233d2b2a32ff4e3991860526b3_369_0.png)

For your purposes, the term reference type is just a fancy name for a class. Because String is defined to be a class in the Java API, I call String a reference type. This terminology highlights the parallel between primitive types (such as int) and classes (that is, reference types, such as String).

## Comparing strings

In the preceding bullets, the difference between int and String is mighty interesting. But if the double equal sign doesn't work for String values, how do you check to see if Joe User enters the correct password? You do it with the code in Listing 18-5.

### Listing 18-5: Calling an Object's Method

```java
/*
* This program works!
*/
import java.util.Scanner;
import static java.lang.System.out;

class CheckPassword {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        String password = "swordfish";
        String userInput;

        out.print("What's the password? ");
        userInput = keyboard.next();

        if (password.equals(userInput)) {
            out.println("You're okay!");
        } else {
            out.println("You're a menace.");
        }

        keyboard.close();
    }
}
```

A run of the new password-checking code is shown in Figure 18-5, and let me tell you, it’s a big relief! The code in Listing 18-5 actually works! When the user types swordfish, the if statement’s condition is true.

![](img/bf4858233d2b2a32ff4e3991860526b3_370_0.png)

**Figure 18-5:** At last, Joe User can log in.

## The truth about classes and methods

The magic in Listing 18-5 is the use of a method named equals. I have two ways to explain the equals method—a simple way, and a more detailed way. First, here’s the simple way: The equals method compares the characters in one string with the characters in another. If the characters are the same, the condition inside the if statement is true. That’s all there is to it.

![](img/bf4858233d2b2a32ff4e3991860526b3_370_1.png)

Don’t use a double equal sign to compare two String objects. Instead, use one of the object’s equals methods.

For a more detailed understanding of the equals method, flip to Chapter 17 and take a look at Figures 17-7 and 17-8. Those figures illustrate the similarities between classes, objects, and the parts of a table. In the figures, each row represents a purchase, and each column represents a feature that purchases possess.

You can observe the same similarities for any class, including Java’s String class. In fact, what Figure 17-7 does for purchases, Figure 18-6 does for strings.

Figure 18-6: Viewing the `String` class as `String` objects as parts of a table.

| **String** |  |  |
|---|---|---|
| **value** | **count** | **equals** |
| `swordfish` | 9 | *(A method to compare `swordfish` with any string)* |
| `catfish` | 7 | *(A method to compare `catfish` with any string)* |

The stuff shown in Figure 18-6 is much simpler than the real `String` class story. But Figure 18-6 makes a good point. Like the purchases in Figure 17-7, each string has its own features. For example, each string has a value (the actual characters stored in the string), and each string has a count (the number of characters stored in the string). You can’t really write the following line of code because the stuff in Figure 18-6 omits a few subtle details.

```java
//This code does NOT work:
System.out.println(password.count);
```

Anyway, each row in Figure 18-6 has three items — a value, a count, and an equals method. So each row of the table contains more than just data. Each row contains an equals method, a way of doing something useful with the data. It’s as though each object (each instance of the `String` class) has three things:

- A bunch of characters (the object’s value)
- A number (the object’s count)
- A way of being compared with other strings (the object’s equals method)

That’s the essence of object-oriented programming. Each string has its own personal copy of the equals method. For example, in Listing 18-5, the password string has its own equals method. When you call the password string’s equals method and put the userInput string in the method’s parentheses, the method compares the two strings to see if those strings contain the same characters.

The userInput string in Listing 18-5 has an equals method, too. I could use the userInput string’s equals method to compare this string with the password string. But I don’t. In fact, in Listing 18-5, I don’t use the userInput string’s equals method at all. (To compare the userInput with the password, I had to use either the password string’s equals method or the userInput string’s equals method. So I made an arbitrary choice: I chose the password string’s method.)

## Calling an object's methods

Calling a string's equals method is like getting a purchase's total. With both equals and total, you use your old friend, the dot. For example, in Listing 17-3, you write

```
System.out.println(onePurchase.total);
```

and in Listing 18-5, you write

```
if (password.equals(userInput))
```

A dot works the same way for an object's variables and its methods. In either case, a dot takes the object and picks out one of the object's parts. It works whether that part is a piece of data (as in onePurchase.total) or a method (as in password.equals).

## Combining and using data

At this point in the chapter, I can finally say, "I told you so." Here's a quotation from Chapter 17:

> A class is a design plan; it describes the way in which you intend to combine and use pieces of data.

A class can define the way you use data. How do you use a password and a user's input? You check to see whether they're the same. That's why Java's String class defines an equals method.

![](img/bf4858233d2b2a32ff4e3991860526b3_372_0.png)

An object can be more than just a bunch of data. With object-oriented programming, each object possesses copies of methods for using that object.

## Static Methods

You have a fistful of checks. Each check has a number, an amount, and a payee. You print checks like these with your very own laser printer. To print the checks, you use a Java class. Each object made from the Check class has three variables (number, amount, and payee). And each object has one method (a print method). You can see all this in Figure 18-7.
