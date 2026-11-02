
## Putting String variables to good use

The program in Listing 18-1 takes the user's input and echoes it back on the screen. This is a wonderful program, but (like many college administrators that I know) it doesn't seem to be particularly useful.

So take a look at a more useful application of Java's String type. A nice one is in Listing 18-2.

## Listing 18-2: Putting a Name in a String Variable

```java
import java.util.Scanner;
import static java.lang.System.out;

class ProcessMoreData {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        String fullName;
        double amount;
        boolean taxable;
        double total;

        out.print("Customer's full name: ");
        fullName = keyboard.nextLine();
        out.print("Amount: ");
        amount = keyboard.nextDouble();
        out.print("Taxable? (true/false) ");
        taxable = keyboard.nextBoolean();

        if (taxable) {
            total = amount * 1.05;
        } else {
            total = amount;
        }

        out.println();
        out.print("The total for ");
        out.print(fullName);
        out.print(" is ");
        out.print(total);
        out.println(".");

        keyboard.close();
    }
}
```

A run of the code in Listing 18-2 is shown in Figure 18-2. The code stores Barry A. Burd in a variable called fullName and displays the fullName variable's content as part of the output. To make this program work, you have to store Barry A. Burd somewhere. After all, the program follows a certain outline:

```
Get a name.
Get some other stuff.
Compute the total.
Display the name (along with some other stuff).
```

![](img/6d9dcff12e52b997f3ad31445b712549_365_0.png)

**Figure 18-2**: Making a purchase.

If you don't have the program store the name somewhere, by the time it's done getting other stuff and computing the total, it forgets the name (so the program can't display the name).

## Reading and writing strings

To read a String value from the keyboard, you can call either next or nextLine:

- The method `next` reads up to the next blank space. For example, with the input Barry A. Burd, the statements
  
  ```java
  String firstName = keyboard.next();
  String middleInit = keyboard.next();
  String lastName = keyboard.next();
  ```
  
  assign Barry to firstName, A. to middleInit, and Burd to lastName.

- The method `nextLine` reads up to the end of the current line. For example, with input Barry A. Burd, the statement
  
  ```java
  String fullName = keyboard.nextLine();
  ```
  
  assigns Barry A. Burd to the variable fullName. (Hey, being an author has some hidden perks.)

## Listing 18-3 *(continued)*

```java
public static void main(String args[]) {
    Scanner keyboard = new Scanner(System.in);
    String password = "swordfish";
    String userInput;

    out.print("What's the password? ");
    userInput = keyboard.next();

    if (password == userInput) {
        out.println("You're okay!");
    } else {
        out.println("You're a menace.");
    }

    keyboard.close();
}
```

**Figure 18-3:** But I typed the correct password!

![](img/6d9dcff12e52b997f3ad31445b712549_367_0.png)

Here are the facts as they appear in this example:

- According to the code in Listing 18-3, the value of `password` is `"swordfish"`.
- In Figure 18-3, in response to the program’s prompt, the user types `swordfish`. So in the code, the value of `userInput` is `"swordfish"`.
- The `if` statement checks the condition `password == userInput`. Because both variables have the value `"swordfish"`, the condition *should* be true, but . . .
- The condition is *not* true because the program’s output is `You're a menace.`

What’s going on here? I try beefing up the code to see if I can find any clues. An enhanced version of the password-checking program is in Listing 18-4, with a run of the new version shown in Figure 18-4.

## Listing 18-4: An Attempt to Debug the Code in Listing 18-3

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

**Figure 18-4:** This looks even worse.

![](img/6d9dcff12e52b997f3ad31445b712549_368_0.png)

Ouch! I'm stumped this time. The run in Figure 18-4 shows that both the userInput and password variables have value swordfish. So why doesn't the program accept the user's input?

```java
out.print("What's the password? ");
userInput = keyboard.next();

if (password.equals(userInput)) {
    out.println("You're okay!");
} else {
    out.println("You're a menace.");
}

keyboard.close();
}
```

A run of the new password-checking code is shown in Figure 18-5, and let me tell you, it's a big relief! The code in Listing 18-5 actually works! When the user types swordfish, the if statement's condition is true.

![](img/6d9dcff12e52b997f3ad31445b712549_370_0.png)

## The truth about classes and methods

The magic in Listing 18-5 is the use of a method named equals. I have two ways to explain the equals method — a simple way, and a more detailed way. First, here's the simple way: The equals method compares the characters in one string with the characters in another. If the characters are the same, the condition inside the if statement is true. That's all there is to it.

![](img/6d9dcff12e52b997f3ad31445b712549_370_1.png)

Don't use a double equal sign to compare two String objects. Instead, use one of the object's equals methods.

For a more detailed understanding of the equals method, flip to Chapter 17 and take a look at Figures 17-7 and 17-8. Those figures illustrate the similarities between classes, objects, and the parts of a table. In the figures, each row represents a purchase, and each column represents a feature that purchases possess.

You can observe the same similarities for any class, including Java's String class. In fact, what Figure 17-7 does for purchases, Figure 18-6 does for strings.

**Figure 18-6**: Viewing the String class and String objects as parts of a table.

**String**

| value | count | equals |
|---|---|---|
| swordfish | 9 | (A method to compare swordfish with any string) |
| catfish | 7 | (A method to compare catfish with any string) |

The stuff shown in Figure 18-6 is much simpler than the real String class story. But Figure 18-6 makes a good point. Like the purchases in Figure 17-7, each string has its own features. For example, each string has a value (the actual characters stored in the string), and each string has a count (the number of characters stored in the string). You can't really write the following line of code because the stuff in Figure 18-6 omits a few subtle details.

```java
//This code does NOT work:
System.out.println(password.count);
```

Anyway, each row in Figure 18-6 has three items — a value, a count, and an equals method. So each row of the table contains more than just data. Each row contains an equals method, a way of doing something useful with the data. It's as though each object (each instance of the String class) has three things:

- A bunch of characters (the object's value)
- A number (the object's count)
- A way of being compared with other strings (the object's equals method)

That's the essence of object-oriented programming. Each string has its own personal copy of the equals method. For example, in Listing 18-5, the password string has its own equals method. When you call the password string's equals method and put the userInput string in the method's parentheses, the method compares the two strings to see if those strings contain the same characters.

The userInput string in Listing 18-5 has an equals method, too. I could use the userInput string's equals method to compare this string with the password string. But I don't. In fact, in Listing 18-5, I don't use the userInput string's equals method at all. (To compare the userInput with the password, I had to use either the password string's equals method or the userInput string's equals method. So I made an arbitrary choice: I chose the password string's method.)
