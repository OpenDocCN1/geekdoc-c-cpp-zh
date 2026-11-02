
## Chapter 17
## Programming with Objects and Classes
### In This Chapter
- Programming with class (and with style and finesse)
- Making objects from classes
- Joining the exclusive "I understand classes and objects" society

Chapters 6, 7, and 8 introduce Java's primitive types — things like int, double, char, and boolean. That's great, but how often does a real-world problem deal exclusively with such simple values? Consider an exchange between a merchant and a customer. The customer makes a purchase, which can involve item names, model numbers, credit card info, sales tax rates, and lots of other stuff.

In older computer programming languages, you treat an entire purchase like a big pile of unbundled laundry. Imagine a mound of socks, shirts, and other pieces of clothing. You have no basket, so you grab as much as you can handle. As you walk to the washer, you drop a few things — a sock here and a washcloth there. This is like the older way of storing the values in a purchase. In older languages, there's no purchase. There are only double values, char values, and other loose items. You put the purchase amount in one variable, the customer's name in another, and the sales tax data somewhere else. But that's awful. You tend to drop things on your way to the compiler. With small errors in a program, you can easily drop an amount here and a customer's name there.

So with laundry and computer programming, you're better off if you have a basket. The newer programming languages, like Java, allow you to combine values and make new, more useful kinds of values. For example, in Java, you can combine double values, boolean values, and other kinds of values to create something that you call a Purchase. Because your purchase info is all in one big bundle, keeping track of the purchase's pieces is easier. That's the start of an important computer programming concept — the notion of object-oriented programming.

## Creating a Class

I start with a “traditional” example. The program in Listing 17-1 processes simple purchase data. Two runs of the program are shown in Figure 17-1.

### Listing 17-1: Doing It the Old Fashioned Way

```java
import java.util.Scanner;

class ProcessData {

    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        double amount;
        boolean taxable;
        double total;

        System.out.print("Amount: ");
        amount = keyboard.nextDouble();
        System.out.print("Taxable? (true/false) ");
        taxable = keyboard.nextBoolean();

        if (taxable) {
            total = amount * 1.05;
        } else {
            total = amount;
        }

        System.out.print("Total: ");
        System.out.println(total);

        keyboard.close();
    }
}
```

![](img/f938eba5f15e231d828a6255e7ec5523_349_0.png)

If the output in Figure 17-1 looks funny, it's because I do nothing in the code to control the number of digits beyond the decimal point. So in the output, the value $20.00 looks like 20.0. That's okay. I show you how to fix the problem in Chapter 18.

## Reference types and Java classes

The code in Listing 17-1 involves a few simple values — amount, taxable, and total. So here's the main point of this chapter: By combining several simple values, you can get a single, more useful value. That's the way it works. You take some of Java's primitive types, whip them together to make a primitive type stew, and what do you get? You get a more useful type called a reference type. Listing 17-2 has an example.

### Listing 17-2: What It Means to Be a Purchase

```java
class Purchase {
    double amount;
    boolean taxable;
    double total;
}
```

The code in Listing 17-2 has no main method, so Eclipse can compile the code, but you can't run it. When you choose Run→Run As in Eclipse's main menu, the resulting context menu has no Java Application entry. You can click the tiny Run As button in Eclipse's toolbar and then select Java Application. But then you get the message box shown in Figure 17-2. Because Listing 17-2 has no main method, there's no place to start the executing. (In fact, the code in Listing 17-2 has no statements at all. There's nothing to execute.)

Figure 17-2:
The code in Listing 17-2 has no main method.

![](img/f938eba5f15e231d828a6255e7ec5523_350_0.png)

## Using a newly defined class

To do something useful with the code in Listing 17-2, you need a main method. You can put the main method in a separate file. Listing 17-3 shows you such a file.

### Listing 17-3: Using Your Purchase Class

```java
import java.util.Scanner;

class ProcessPurchase {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        Purchase onePurchase = new Purchase();

        System.out.print("Amount: ");
        onePurchase.amount = keyboard.nextDouble();
        System.out.print("Taxable? (true/false) ");
        onePurchase.taxable = keyboard.nextBoolean();

        if (onePurchase.taxable) {
            onePurchase.total = onePurchase.amount * 1.05;
        } else {
            onePurchase.total = onePurchase.amount;
        }

        System.out.print("Total: ");
        System.out.println(onePurchase.total);

        keyboard.close();
    }
}
```

The best way to understand the code in Listing 17-3 is to compare it, line by line, with the code in Listing 17-1. In fact, there's a mechanical formula for turning the code in Listing 17-1 into the code in Listing 17-3. Table 17-1 describes the formula.

### Table 17-1 Converting Your Code to Use a Class

| In Listing 17-1 | In Listing 17-3 |
|---|---|
| double amount; boolean taxable; double total; | Purchase onePurchase = new Purchase(); |
| amount | onePurchase.amount |
| taxable | onePurchase.taxable |
| total | onePurchase.total |

The two programs (in Listings 17-1 and 17-3) do essentially the same thing, but one uses primitive variables, and the other leans on the Purchase code from Listing 17-2. Both programs have runs like the ones shown back in Figure 17-1.

## From Classes Come Objects

The code in Listing 17-2 defines a class. A class is a design plan; it describes the way in which you intend to combine and use pieces of data. For example, the code in Listing 17-2 announces your intention to combine double, boolean, and double values to make new Purchase values.

Classes are central to all Java programming. But Java is called an object-oriented language. Java isn’t called a class-oriented language. In fact, no one uses the term class-oriented language. Why not?

Well, you can’t put your arms around a class. A class isn’t real. A class without an object is like a day without chocolate. If you’re sitting in a room right now, glance at all the chairs in the room. How many chairs are in the room? Two? Five? Twenty? In a room with five chairs, you have five chair objects. Each chair (each object) is something real, something you can use, something you can sit on.

A language like Java has classes and objects. So what’s the difference between a class and an object?

- An object is a thing.
- A class is a design plan for things of that kind.

For example, how would you describe what a chair is? Well, a chair has a seat, a back, and legs. In Java, you may write the stuff in Listing 17-4.

### Listing 17-4: What It Means to Be a Chair

```java
/*
 * This is real Java code, but this code
 * cannot be compiled on its own:
 */

class Chair {
    FlatHorizontalPanel seat;
    FlatVerticalPanel back;
    LongSkinnyVerticalRods legs;
}
```

The preceding code is a design plan for chairs. The code tells you that each chair has three things. The code names the things (seat, back, and legs) and tells you a little bit about each thing. (For example, a seat is a FlatHorizontalPanel.) In the same way, the code in Listing 17-2 tells you that each purchase has three things. The code names the things (amount, taxable, and total) and tells you the primitive type of each thing.

So imagine some grand factory at the edge of the universe. While you sleep each night, this factory stamps out tangible objects — objects that you'll encounter during the next waking day. Tomorrow you'll go for an interview at the Sloshy Shoes Company. So tonight, the factory builds chairs for the company's offices. The factory builds chair objects, as shown in Figure 17-3, from the almost-real code in Listing 17-4.

### Figure 17-3: Chair objects from the Chair class.

![](img/f938eba5f15e231d828a6255e7ec5523_354_0.png)

In Listing 17-3, the line

```java
Purchase onePurchase = new Purchase();
```

behaves like that grand factory at the edge of the universe. Instead of creating chair objects, that line in Listing 17-3 creates a purchase object, as shown in Figure 17-4. That particular line in Listing 17-3 is a declaration with an initialization. Just as the line

```java
int count = 0;
```

declares the count variable and sets count to 0, the line in Listing 17-3 declares the onePurchase variable and makes onePurchase point to a brand-new object. That new object contains three parts: an amount part, a taxable part, and a total part.
