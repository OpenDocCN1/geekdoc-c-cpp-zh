
```java
Scanner diskScanner =
    new Scanner(new File("occupancy"));
int guestsIn[];
guestsIn = new int[10];

for (int roomNum = 0; roomNum < 10; roomNum++) {
    guestsIn[roomNum] = diskScanner.nextInt();
}

for (int roomNum = 9; roomNum >= 0; roomNum--) {
    if (guestsIn[roomNum] == 0) {
        System.out.print("Room ");
        System.out.print(roomNum);
        System.out.println(" is vacant.");
    }
}

diskScanner.close();
}
```

Notice the stuff in parentheses in the VacanciesInReverse program's second for loop. It's easy to get these things wrong. You're aiming for a loop that checks Room 9, then Room 8, and so on.

```java
if (guestsIn[9] == 0) {
    System.out.print(roomNum);
}
if (guestsIn[8] == 0) {
    System.out.print(roomNum);
}
if (guestsIn[7] == 0) {
    System.out.print(roomNum);
}
```

...And so on, until you get to...

```java
if (guestsIn[0] == 0) {
    System.out.print(roomNum);
}
```

Some observations about the code:

- ✓ The loop's counter must start at 9: `for (int roomNum = 9; roomNum >= 0; roomNum--)`
- Each time through the loop, the counter goes down by one: `for (int roomNum = 9; roomNum >= 0; roomNum--)`
- The loop keeps going as long as the counter is greater than or equal to 0: `for (int roomNum = 9; roomNum >= 0; roomNum--)`

Think through each of these three items, and you'll write a perfect for loop.

## Working with Arrays

Earlier in this chapter, a busload of loners showed up at your motel. When they finally left, you were glad to get rid of them, even if it meant having all your rooms empty for a while. But now, another bus pulls into the parking lot. This bus has a sign that says "Gregarian Club." Out of the bus come 50 people, each more gregarious than the next. Now everybody in your parking lot is clamoring to meet everyone else. While they meet and greet, they're all frolicking toward the front desk, singing the club's theme song. (Oh no! It's the Gregarian Chant!)

The first five Gregarians all want Room 7. It's a tight squeeze, but you were never big on fire codes, anyway. Next comes a group of three with a yen for Room 0. (They're computer programmers, and they think the room number is cute.) Then there's a pack of four Gregarians who want Room 3. (The in-room pool sounds attractive to them.)

With all this traffic, you better switch on your computer. You start a program that enables you to enter new occupancy data. The program has five parts:

### Create an array and then put 0 in each of the array's components.

When the Loners' Club members left, the motel was suddenly empty. (Heck, even before the Loners' Club members left, the motel seemed empty.) To declare an array and fill the array with zeros, you execute code of the following kind:

```java
int guestsIn[];
guestsIn = new int[10];

for (int roomNum = 0; roomNum < 10; roomNum++) {
    guestsIn[roomNum] = 0;
}
```

### Get a room number and then get the number of guests who will be staying in that room.

Reading numbers typed by the user is pretty humdrum stuff. Do a little prompting and a little nextInt calling, and you're all set:

```java
out.print("Room number: ");
whichRoom = keyboard.nextInt();
out.print("How many guests? ");
numGuests = keyboard.nextInt();
```

### Use the room number and the number of guests to change a value in the array.

Earlier in this chapter, to put one guest in Room 2, you executed

```java
guestsIn[2] = 1;
```

So now, you have two variables — numGuests and whichRoom. Maybe numGuests is 5, and whichRoom is 7. To put numGuests in whichRoom (that is, to put 5 guests in Room 7), you can execute

```java
guestsIn[whichRoom] = numGuests;
```

That's the crucial step in the design of your new program.

### Ask the user if the program should keep going.

Are there more guests to put in rooms? To find out, execute this code:

```java
out.print("Do another? ");
} while (keyboard.findWithinHorizon(".",0).charAt(0) == 'Y');
```

### Display the number of guests in each room.

No problem! You already did this. You can steal the code (almost verbatim) from Listing 16-1:

```java
out.println("Room\tGuests");
for (int roomNum = 0; roomNum < 10; roomNum++) {
    out.print(roomNum);
    out.print("\t");
    out.println(guestsIn[roomNum]);
}
```

The only difference between this latest code snippet and the stuff in Listing 16-1 is that this new code uses the guestsIn array. The first time through this loop, the code does

```java
out.println(guestsIn[0]);
```

displaying the number of guests in Room 0. The next time through the loop, the code does

```java
out.println(guestsIn[1]);
```

displaying the number of guests in Room 1. The last time through the loop, the code does

```java
out.println(guestsIn[9]);
```

That's perfect.

The complete program (with these five pieces put together) is in Listing 16-5. A run of the program is shown in Figure 16-7.

### Listing 16-5: Storing Occupancy Data in an Array

```java
import java.util.Scanner;
import static java.lang.System.out;

class AddGuests {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        int whichRoom, numGuests;
        int guestsIn[];
        guestsIn = new int[10];

        for (int roomNum = 0; roomNum < 10; roomNum++) {
            guestsIn[roomNum] = 0;
        }

        do {
            out.print("Room number: ");
            whichRoom = keyboard.nextInt();
            out.print("How many guests? ");
            numGuests = keyboard.nextInt();
            guestsIn[whichRoom] = numGuests;

            out.println();
            out.print("Do another? ");
        } while (keyboard.findWithinHorizon(".",0).charAt(0) == 'Y');

        out.println();
        out.println("Room\tGuests");
        for (int roomNum = 0; roomNum < 10; roomNum++) {
            out.print(roomNum);
            out.print("\t");
            out.println(guestsIn[roomNum]);
        }

        keyboard.close();
    }
}
```

![](img/6d9dcff12e52b997f3ad31445b712549_342_0.png)

Figure 16-7: Running the code in Listing 16-5.

Hey! The program in Listing 16-5 is pretty big! It may be the biggest program so far in this book. But big doesn't necessarily mean difficult. If each piece of the program makes sense, you can create each piece on its own, and then put all the pieces together. Voilà! The code is manageable.

## Looping in Style

Chapter 15's Listing 15-6 uses an enhanced for loop to step through a bunch of values. In that program, the values belong to an enum type. Well, this chapter also deals with a bunch of values — namely, the values in an array. So you're probably not surprised if I show you an enhanced for loop that steps through an array's values.

To see such a loop, start with the code in Listing 16-5. The last loop in that program looks something like this:

```java
for (int roomNum = 0; roomNum < 10; roomNum++) {
    out.println(guestsIn[roomNum]);
}
```

To turn this into an enhanced for loop, you make up a new variable name. (What about the name `howMany`? I like that name.) Whatever name you choose, the new variable ranges over the values in the `guestsIn` array.

```java
for (int howMany : guestsIn) {
    out.println(howMany);
}
```

This enhanced loop uses the same format as the loop in Chapter 15.

```java
for (TypeName variableName : RangeOfValues) {
    Statements
}
```

In Chapter 15, the `RangeOfValues` belongs to an enum type. But in this chapter's example, the `RangeOfValues` belongs to an array.

Enhanced for loops are nice and concise. But don't be too anxious to use enhanced loops with arrays. This feature has some nasty limitations. For example, my new howMany loop doesn't display room numbers. I avoid room numbers because the room numbers in my guestsIn array are the indices 0 through 9. Unfortunately, an enhanced loop doesn't provide easy access to an array's indices.

And here's another unpleasant surprise. Start with the following loop from Listing 16-4:

```java
for (int roomNum = 0; roomNum < 10; roomNum++) {
    guestsIn[roomNum] = diskScanner.nextInt();
}
```

Turn this traditional for loop into an enhanced for loop, and you get the following misleading code:

```java
for (int howMany : guestsIn) {
    howMany = diskScanner.nextInt();    //Don't do this
}
```

The new enhanced loop doesn't do what you want it to do. This loop reads values from an input file and then dumps these values into the garbage can. In the end, the array's values remain unchanged.

It's sad but true. To make full use of an array, you have to fall back on Java's plain old for loop.
