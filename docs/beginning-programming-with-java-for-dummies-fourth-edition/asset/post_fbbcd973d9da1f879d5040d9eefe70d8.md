
Because the kids and seniors' prices are the same, you can combine these prices into one category. (That's not always the best programming strategy, but do it anyway for this example.) To find a particular moviegoer's ticket price, you need one or more if statements. You can structure the conditions in many ways, and I chose one of these ways for the code in Listing 10-1.

## Listing 10-1: Are You Paying Too Much?

```java
import java.util.Scanner;

class TicketPrice {

    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        int age;
        double price = 0.00;

        System.out.print("How old are you? ");
        age = keyboard.nextInt();

        if (age >= 12 && age < 65) {
            price = 9.25;
        }
        if (age < 12 || age >= 65) {
            price = 5.25;
        }

        System.out.print("Please pay $");
        System.out.print(price);
        System.out.print(".");
        System.out.println("Enjoy the show!");

        keyboard.close();
    }
}
```

Several runs of the TicketPrice program (refer to Listing 10-1) are shown in Figure 10-2. (For your viewing pleasure, I've copied the runs from Eclipse's Console view to Windows Notepad.) When you turn 12, you start paying full price. You keep paying the full price until you become 65. At that point, you pay the reduced price again.

The pivotal part of Listing 10-1 is the lump of if statements in the middle, which are illustrated in Figure 10-3.

## Figure 10-2:
Admission prices for Beginning Programming with Java For Dummies: The Movie.

```
How old are you? 11
Please pay $5.25. Enjoy the show!

How old are you? 12
Please pay $9.25. Enjoy the show!

How old are you? 35
Please pay $9.25. Enjoy the show!

How old are you? 64
Please pay $9.25. Enjoy the show!

How old are you? 65
Please pay $5.25. Enjoy the show!
```

## Figure 10-3:
The meanings of the conditions in Listing 10-1.

![](img/6d9dcff12e52b997f3ad31445b712549_212_0.png)

- The first if statement's condition tests for the regular price group. Anyone who's at least 12 years of age and is under 65 belongs in this group.
- The second if statement's condition tests for the fringe ages. A person who's under 12 or is 65 or older belongs in this category.

![](img/6d9dcff12e52b997f3ad31445b712549_212_1.png)

When you form the opposite of an existing condition, you can often follow the pattern in Listing 10-1. The opposite of >= is <. The opposite of < is >=. The opposite of && is ||.

![](img/6d9dcff12e52b997f3ad31445b712549_212_2.png)

If you change the dollar amounts in Listing 10-1, you can get into trouble. For example, with the statement price = 5.00, the program displays Please pay $5.0. Enjoy the show! This happens because Java doesn't store the two zeros to the right of the decimal point (and Java doesn't know or care that 5.00 is a dollar amount). To fix this kind of thing, see the discussion of NumberFormat.getCurrencyInstance in Chapter 18.

## When to initialize?

Take a look at Listing 10-1 and notice the price variable's initialization:

```
double price = 0.00;
```

This line declares the price variable and sets the variable's starting value to 0.00. When I omit this initialization, I get an error message:

```
The local variable price may not have been initialized
```

What's the deal here? I don't initialize the age variable, but the compiler doesn't complain about that. Why is the compiler fussing over the price variable?

The answer is in the placement of the code's assignment statements. Consider the following two facts:

- **The statement that assigns a value to age (age = keyboard.nextInt()) isn't inside an if statement.**
  
  That assignment statement always gets executed, and (as long as nothing extraordinary happens) the variable age is sure to be assigned a value.
  
- **Both statements that assign a value to price (price = 9.25 and price = 5.25) are inside if statements.**

If you look at Figure 10-3, you see that every age group is covered. No one shows up at the ticket counter with an age that forces both if conditions to be false. So, whenever you run the TicketPrice program, either the first or the second price assignment is executed.

The problem is that the compiler isn't smart enough to check all this. The compiler just sees the structure in Figure 10-4 and becomes scared that the computer won't take either of the true detours.

If (for some unforeseen reason) both of the if statements' conditions are false, then the variable price isn't assigned a value. So without an initialization, price has no value. (More precisely, price has no value that's intentionally given to it in the code.)

Eventually, the computer reaches the System.out.print(price) statement. It can't display price unless price has a meaningful value. So at that point, the compiler throws up its virtual hands in disgust.

![](img/6d9dcff12e52b997f3ad31445b712549_214_0.png)

Figure 10-4:
The choices
in Listing
10-1.

## More and more conditions

Last night I had a delicious meal at the neighborhood burger joint. As part of a promotion, I got a discount coupon along with the meal. The coupon is good for $2.00 off the price of a ticket at the local movie theater.

To make use of the coupon in the TicketPrice program, I have to tweak the code in Listing 10-1. The revised code is in Listing 10-2. In Figure 10-5, I take that new code around the block a few times.

## Figure 10-5
Running the code in Listing 10-2

How old are you? 51
Have a coupon? (Y/N) Y
Please pay $7.25. Enjoy the show!

How old are you? 51
Have a coupon? (Y/N) y
Please pay $7.25. Enjoy the show!

How old are you? 51
Have a coupon? (Y/N) N
Please pay $9.25. Enjoy the show!

How old are you? 51
Have a coupon? (Y/N) X
Huh?
Please pay $9.25. Enjoy the show!

## Listing 10-2: Do You Have a Coupon?

```java
import java.util.Scanner;

class TicketPriceWithDiscount {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        int age;
        double price = 0.00;
        char reply;

        System.out.print("How old are you? ");
        age = keyboard.nextInt();

        System.out.print("Have a coupon? (Y/N) ");
        reply = keyboard.findWithinHorizon(".", 0).charAt(0);

        if (age >= 12 && age < 65) {
            price = 9.25;
        }
        if (age < 12 || age >= 65) {
            price = 5.25;
        }

        if (reply == 'Y' || reply == 'y') {
            price -= 2.00;
        }
        if (reply != 'Y' && reply != 'y' && reply!='N' && reply!='n') {
            System.out.println("Huh?");
        }
    }
}
```

```
System.out.print("Please pay $");
System.out.print(price);
System.out.print(".\n");
System.out.println("Enjoy the show!");
    keyboard.close();
}
```

Listing 10-2 has two if statements whose conditions involve characters:

- In the first such statement, the computer checks to see whether the reply variable stores the letter Y or the letter y. If either is the case, it subtracts 2.00 from the price. (For information on operators like -=, see Chapter 7.)
- The second such statement has a hefty condition. The condition tests to see whether the reply variable stores any reasonable value at all. If the reply isn't Y, and isn't y, and isn't N, and isn't n, the computer expresses its concern by displaying, "Huh?" (As a paying customer, the word "Huh?" on the automated ticket teller's screen will certainly get your attention.)

![](img/6d9dcff12e52b997f3ad31445b712549_216_0.png)

When you create a big multipart condition, you always have several ways to think about the condition. For example, you can rewrite the last condition in Listing 10-2 as if (! (reply == 'Y' || reply == 'y' || reply == 'N' || reply == 'n')). If it's not the case that the reply is either Y, y, N, or n, then display 'Huh?' So which way of writing the condition is better — the way I do it in Listing 10-2, or the way I do it in this tip? It depends on your taste. Whichever makes the logic easier for you to understand is the better way.

## Using boolean variables

No matter how good a program is, you can always make it a little bit better. Take the code in Listing 10-2. Does the forest of if statements make you nervous? Do you slow to a crawl when you read each condition? Wouldn't it be nice if you could glance at a condition and make sense of it very quickly?

To some extent, you can. If you're willing to create some additional variables, you can make your code easier to read. Listing 10-3 shows you how.
