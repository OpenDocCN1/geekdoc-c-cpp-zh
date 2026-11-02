
![](img/f938eba5f15e231d828a6255e7ec5523_355_0.png)

Figure 17-4:
An object created from the Purchase class.

![](img/f938eba5f15e231d828a6255e7ec5523_355_1.png)

If you want to be picky, there's a difference between the stuff in Figure 17-4 and the action of the big bold statement in Listing 17-3. Figure 17-4 shows an object with the values 20.00, true, and 21.00 stored in it. The statement in Listing 17-3 creates a new object, but it doesn't fill the object with useful values. Getting values comes later in Listing 17-3.

## Understanding (or ignoring) the subtleties

Sometimes, when you refer to a particular object, you want to emphasize which class the object came from. Well, subtle differences in emphasis call for big differences in terminology. So here's how Java programmers use the terminology:

- The bold line in Listing 17-3 creates a new object.
- The bold line in Listing 17-3 creates a new instance of the Purchase class.

The words object and instance are almost synonymous, but Java programmers never say "object of the Purchase class" (or if they do, they feel funny).

By the way, if you mess up this terminology and say something like "object of the Purchase class," no one jumps down your throat. Everyone understands what you mean, and life goes on as usual. In fact, I often use a phrase like "Purchase object" to describe an instance of the Purchase class. The

## Create and enhance masks and mask layers

Use selection tools to create masks, refine them with Select and Mask, and enhance with layers

![](img/f938eba5f15e231d828a6255e7ec5523_356_0.png)

- 1. Selection tools (Marquee, Lasso, Quick Selection, Magic Wand) create masks
- 2. Select and Mask workspace refines mask edges
- 3. Layer masks adjust visibility non-destructively
- 4. Vector masks create sharp, scalable edges

Learn how to create masks to hide or reveal parts of a layer, combine multiple images, and apply targeted edits.

> Masking is an essential skill for non-destructive editing.

| Purchase |  |  |
|---|---|---|
| amount | taxable | total |
| 20.00 | true | 21.00 |
| 20.00 | false | 20.00 |
| 95.00 | true | 99.75 |

```
aPurchase = new Purchase();
...
aPurchase.amount = myScanner.nextDouble();
...
aPurchase.taxable = myScanner.nextBoolean();
...
aPurchase.total = aPurchase.amount * 1.05;
```

Figure 17-8: A purchase corresponds to a row of the table.

## Some questions and answers

Here’s the world’s briefest object-oriented programming FAQ:

- **Can I have an object without having a class?**
  No, you can’t. In Java, every object is an instance of a class.

- **Can I have a class without having an object?**
  Yes, you can. In fact, almost every program in this book creates a class without an object. Take Listing 17-5, for example. The code in Listing 17-5 defines a class named ProcessPurchase. And nowhere in Listing 17-5 (or anywhere else) do I create an instance of the ProcessPurchase class. I have a class with no objects. That’s just fine. It’s business as usual.

- **After I’ve created a class and its instances, can I add more instances to the class?**
  Yes, you can. In Listing 17-5, I create one instance, then another, and then a third. If I went one additional time around the for loop, I’d have a fourth instance, and I’d put a fourth row in the table of Figure 17-8. With no objects, three objects, four objects, or more objects, I still have the same old Purchase class.

- **Can an object come from more than one class?**
  Bite your tongue! Maybe other object-oriented languages allow this nasty class cross-breeding, but in Java, it’s strictly forbidden. That’s one of the things that distinguishes Java from some of the languages that preceded it. Java is cleaner, more uniform, and easier to understand.

## Chapter 18

## Using Methods and Variables from a Java Class

## In This Chapter

- Using Java’s String class
- Calling methods
- Understanding static and non-static methods and variables
- Making numbers look good

I hope you didn’t read Chapter 17 because I tell a big lie at the beginning of the chapter. Actually, it’s not a lie. It’s an exaggeration.

Actually, it’s not an exaggeration. It’s a careful choice of wording. In Chapter 17, I write that the gathering of data into a class is the start of object-oriented programming. Well, that’s true. Except that many programming languages had data-gathering features before object-oriented programming became popular. Pascal had records. C had structs.

To be painfully precise, the grouping of data into usable chunks is only a prerequisite to object-oriented programming. You’re not really doing object-oriented programming until you combine both data and methods in your classes.

This chapter starts the “data and methods” ball rolling, and Chapter 19 rounds out the picture.

## The String Class

The String class is declared in the Java API. This means that somewhere in the stuff you download from java.com is a file named String.java. If you hunt down this String.java file and peek at the file’s code, you find some very familiar-looking stuff:

```
class String {
    ...And so on...
```

A run of the code in Listing 18-2 is shown in Figure 18-2. The code stores Barry A. Burd in a variable called fullName and displays the fullName variable's content as part of the output. To make this program work, you have to store Barry A. Burd somewhere. After all, the program follows a certain outline:

```
Get a name.
Get some other stuff.
Compute the total.
Display the name (along with some other stuff).
```

![](img/f938eba5f15e231d828a6255e7ec5523_365_0.png)

Figure 18-2:
Making a purchase.

If you don't have the program store the name somewhere, by the time it's done getting other stuff and computing the total, it forgets the name (so the program can't display the name).

## Reading and writing strings

To read a String value from the keyboard, you can call either next or nextLine:

The method next reads up to the next blank space.

```
String firstName = keyboard.next();
String middleInit = keyboard.next();
String lastName = keyboard.next();
```

assign Barry to firstName, A. to middleInit, and Burd to lastName.

The method nextLine reads up to the end of the current line.

```
String fullName = keyboard.nextLine();
```

assigns Barry A. Burd to the variable fullName. (Hey, being an author has some hidden perks.)

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
        out.print("You typed           ");
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

![](img/f938eba5f15e231d828a6255e7ec5523_368_0.png)

Figure 18-4:
This looks
even worse.

Ouch! I'm stumped this time. The run in Figure 18-4 shows that both the userInput and password variables have value swordfish. So why doesn't the program accept the user's input?

```
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

Figure 18-5:
At last, Joe
User can
log in.

![](img/f938eba5f15e231d828a6255e7ec5523_370_0.png)

## The truth about classes and methods

The magic in Listing 18-5 is the use of a method named equals. I have two ways to explain the equals method — a simple way, and a more detailed way. First, here's the simple way: The equals method compares the characters in one string with the characters in another. If the characters are the same, the condition inside the if statement is true. That's all there is to it.

![](img/f938eba5f15e231d828a6255e7ec5523_370_1.png)

Don't use a double equal sign to compare two String objects. Instead, use one of the object's equals methods.

For a more detailed understanding of the equals method, flip to Chapter 17 and take a look at Figures 17-7 and 17-8. Those figures illustrate the similarities between classes, objects, and the parts of a table. In the figures, each row represents a purchase, and each column represents a feature that purchases possess.

You can observe the same similarities for any class, including Java's String class. In fact, what Figure 17-7 does for purchases, Figure 18-6 does for strings.
