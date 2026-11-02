
## Figure 16-4 The bad room number 10 gets no response.

![](img/6d9dcff12e52b997f3ad31445b712549_332_0.png)

![](img/6d9dcff12e52b997f3ad31445b712549_332_1.png)

In Listing 16-3, I want to know if the occupancy file contains any more data (any data that I haven't read yet). So I call the Scanner class's hasNext method. The hasNext method looks ahead to see whether I can read any kind of data — an int value, a double value, a word, a boolean, or whatever. That's okay for this section's example, but in some situations, you need to be pickier about your input data. For example, you may want to know if you can call nextInt (as opposed to nextDouble or nextLine). Fortunately, Java has methods for your pickiest input needs. A method like diskScanner.hasNextInt() tests to see whether you can read an int value from the disk file. Java also has methods like hasNextLine, hasNextDouble, and so on. For more information on the plain old hasNext method, see Chapter 14.

Listing 16-3 has a big fat condition to keep the for loop going:

```java
for (int roomNum = 0;
    roomNum < whichRoom && diskScanner.hasNext();
    roomNum++) {
```

Many for loop conditions are simple "less-than" tests, but there's no rule saying that all for loop conditions have to be so simple. In fact, any expression can be a for loop's condition, as long as the expression has value true or false. The condition in Listing 16-3 combines a "less than" with a call to the Scanner class's hasNext method.

## Reader, Meet Arrays; Arrays, Meet the Reader

A weary traveler steps up to the Java Motel's front desk. "I'd like a room," says the traveler. So the desk clerk runs a report like the one in Figure 16-2. Noticing the first vacant room in the list, the clerk suggests Room 2. "I'll take it," says the traveler.

It's so hard to get good help these days. How many times have you told the clerk to fill the higher numbered rooms first? The lower numbered rooms are older, and they are badly in need of repair. For example, Room 3 has an indoor pool. (The pipes leak, so the carpet is soaking wet.) Room 2 has no heat (not in wintertime, anyway). Room 1 has serious electrical problems (so, for that room, you always get payment in advance). Besides, Room 8 is vacant, and you charge more for the higher numbered rooms.

Here's where a subtle change in presentation can make a big difference. You need a program that lists vacant rooms in reverse order. That way, Room 8 catches the clerk's eye before Room 2 does.

Think about strategies for a program that displays data in reverse. With the input from Figure 16-1, the program's output should look like the display shown in Figure 16-5.

![](img/6d9dcff12e52b997f3ad31445b712549_333_0.png)

Here's the first (bad) idea for a programming strategy:

```text
Get the last value in the occupancy file.
If the value is 0, print the room number.

Get the next-to-last value in the occupancy file.
If the value is 0, print the room number.

...And so on.
```

With some fancy input/output programs, this strategy may be workable. But no matter what input/output program you use, jumping directly to the end or to the middle of a file is a big pain in the butt. It's especially bad if you plan to jump repeatedly. So go back to the drawing board and think of something better.

Here's an idea! Read all the values in the occupancy file and store each value in a variable of its own. Then you step through the variables in reverse order, displaying a room number when it's appropriate to do so.

This idea works, but the code is so ugly that I refuse to dignify it by calling it a "Listing." No, this is just a "see the following code" kind of thing. So please, see the following ugly code:

```java
/*
 * Ugh! I can't stand this ugly code!
 */
guestsIn0 = diskScanner.nextInt();
guestsIn1 = diskScanner.nextInt();
guestsIn2 = diskScanner.nextInt();
guestsIn3 = diskScanner.nextInt();
guestsIn4 = diskScanner.nextInt();
guestsIn5 = diskScanner.nextInt();
guestsIn6 = diskScanner.nextInt();
guestsIn7 = diskScanner.nextInt();
guestsIn8 = diskScanner.nextInt();
guestsIn9 = diskScanner.nextInt();

if (guestsIn9 == 0) {
    System.out.println(9);
}
if (guestsIn8 == 0) {
    System.out.println(8);
}
if (guestsIn7 == 0) {
    System.out.println(7);
}
if (guestsIn6 == 0) {
// ... And so on.
```

What you're lacking is a uniform way of naming ten variables. That is, it would be nice to write

```java
/*
 * Nice idea, but this is not real Java code:
 */

//Read forwards
for (int roomNum = 0; roomNum < 10; roomNum++) {
    guestsInroomNum = diskScanner.nextInt();
}

//Write backwards
for (int roomNum = 9; roomNum >= 0; roomNum--) {
    if (guestsInroomNum == 0) {
        System.out.println(roomNum);
    }
}
```

Well, you can write loops of this kind. All you need are some square brackets. When you add square brackets to the idea shown in the preceding code, you get what's called an *array*. An *array* is a row of values, like the row of rooms in a one-floor motel. To picture the array, just picture the Java Motel:

- First, picture the rooms, lined up next to one another.
- Next, picture the same rooms with their front walls missing. Inside each room, you can see a certain number of guests.
- If you can, forget that the two guests in Room 9 are putting piles of bills into a big briefcase. Ignore the fact that the guest in Room 5 hasn't moved away from the TV set in a day and a half. Instead of all these details, just see numbers. Each room, see a number representing the count of guests in that room. (If freeform visualization isn't your strong point, take a look at Figure 16-6.)

![](img/6d9dcff12e52b997f3ad31445b712549_335_0.png)

In the lingo of Java programming, the entire row of rooms is called an *array*. Each room in the array is called a *component* of the array (also known as an *array element*). Each component has two numbers associated with it.

- **Index:** In the case of the Java Motel array, the index is the room number (a number from 0 to 9).
- **Value:** In the Java Motel array, the value is the number of guests in a given room (a number stored in a component of the array).

Using an array saves you from having to declare ten separate variables: guestsIn0, guestsIn1, guestsIn2, and so on. To declare an array with ten values in it, you can write two fairly short lines of code:

```java
int guestsIn[];
guestsIn = new int[10];
```

You can even squish these two lines into one longer line:

```java
int guestsIn[] = new int[10];
```

In either of these code snippets, notice the use of the number 10. This number tells the computer to make the guestsIn array have ten components. Each component of the array has a name of its own. The starting component is named guestsIn[0], the next is named guestsIn[1], and so on. The last of the ten components is named guestsIn[9].

![](img/6d9dcff12e52b997f3ad31445b712549_336_0.png)

In creating an array, you always specify the number of components. The array's indices always start with 0 and end with the number that's one fewer than the total number of components. For example, if your array has ten components (and you declare the array with new int[10]), the array's indices go from 0 to 9.

### Storing values in an array

After you've created an array, you can put values into the array's components. For example, the guests in Room 6 are fed up with all those mint candies that you put on people's beds. So they check out, and Room 6 becomes vacant. You should put the value 0 into the 6th component. You can do it with this assignment statement:

```java
guestsIn[6] = 0;
```

On one weekday, business is awful. No one's staying at the motel. But then you get a lucky break. A big bus pulls up to the motel. The side of the bus has a sign that says "Loners' Convention." Out of the bus come 25 people, each walking to the motel's small office, none paying attention to the others who were on the bus. Each person wants a private room. Only 10 of them can stay at the Java Motel, but that's okay, because you can send the other 15 loners down the road to the old C-Side Resort and Motor Lodge.

Anyway, to register ten of the loners into the Java Motel, you put one guest in each of your ten rooms. Having created an array, you can take advantage of the array's indexing and write a for loop, like this:

```java
for (int roomNum = 0; roomNum < 10; roomNum++) {
    guestsIn[roomNum] = 1;
}
```
