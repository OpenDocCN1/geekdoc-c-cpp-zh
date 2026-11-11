
You must first initialize the deadline variable. You have two choices. Of course, you can initialize the variable so that it refers to a newly constructed object:

```java
deadline = new Date();
```

Or you can set the variable to refer to an existing object:

```java
deadline = birthday;
```

Now both variables refer to the *same* object (see Figure 4.4).

![](img/127bccebb2cfadea3f02579edaad63c3_160_0.png)

**Figure 4.4** Object variables that refer to the same object

It is important to realize that an object variable doesn’t actually contain an object. It only *refers* to an object.

In Java, the value of any object variable is a reference to an object that is stored elsewhere. The return value of the new operator is also a reference. A statement such as

```java
Date deadline = new Date();
```

has two parts. The expression `new Date()` makes an object of type Date, and its value is a reference to that newly created object. That reference is then stored in the deadline variable.

You can explicitly set an object variable to `null` to indicate that it currently refers to no object.

```java
deadline = null;

if (deadline != null)
    System.out.println(deadline);
```

We will discuss `null` in more detail in Section 4.3.6, “Working with `null` References,” on p. 148.

> **C++ NOTE:** Some people mistakenly believe that Java object variables behave like C++ references. But in C++ there are no null references, and references cannot be assigned. You should think of Java object variables as analogous to object pointers in C++. For example,
>
>     Date birthday; // Java
>
> is really the same as
>
>     Date* birthday; // C++
>
> Once you make this association, everything falls into place. Of course, a `Date*` pointer isn't initialized until you initialize it with a call to `new`. The syntax is almost the same in C++ and Java.
>
>     Date* birthday = new Date(); // C++
>
> If you copy one variable to another, then both variables refer to the same date—they are pointers to the same object. The equivalent of the Java `null` reference is the C++ `NULL` pointer.

All Java objects live on the heap. When an object contains another object variable, it contains just a pointer to yet another heap object.

In C++, pointers make you nervous because they are so error-prone. It is easy to create bad pointers or to mess up memory management. In Java, these problems simply go away. If you use an uninitialized pointer, the runtime system will reliably generate a runtime error instead of producing random results. You don't have to worry about memory management, because the garbage collector takes care of it.

C++ makes quite an effort, with its support for copy constructors and assignment operators, to allow the implementation of objects that copy themselves automatically. For example, a copy of a linked list is a new linked list with the same contents but with an independent set of links. This makes it possible to design classes with the same copy behavior as the built-in types. In Java, you must use the `clone` method to get a complete copy of an object.

### 4.2.2 The LocalDate Class of the Java Library

In the preceding examples, we used the `Date` class that is a part of the standard Java library. An instance of the `Date` class has a state—namely, *a particular point in time*. Although you don’t need to know this when you use the Date class, the time is represented by the number of milliseconds (positive or negative) from a fixed point, the so-called *epoch*, which is 00:00:00 UTC, January 1, 1970. UTC is the Coordinated Universal Time, the scientific time standard which is, for practical purposes, the same as the more familiar GMT, or Greenwich Mean Time.

But as it turns out, the Date class is not very useful for manipulating the kind of calendar information that humans use for dates, such as “December 31, 1999”. This particular description of a day follows the Gregorian calendar, which is the calendar used in most countries of the world. The same point in time would be described quite differently in the Chinese or Hebrew lunar calendars, not to mention the calendar used by your customers from Mars.

> **NOTE:** Throughout human history, civilizations grappled with the design of calendars to attach names to dates and bring order to the solar and lunar cycles. For a fascinating explanation of calendars around the world, from the French Revolutionary calendar to the Mayan long count, see *Calendrical Calculations* by Nachum Dershowitz and Edward M. Reingold (Cambridge University Press, 3rd ed., 2007).

The library designers decided to separate the concerns of keeping time and attaching names to points in time. Therefore, the standard Java library contains two separate classes: the Date class, which represents a point in time, and the `LocalDate` class, which expresses days in the familiar calendar notation. Java 8 introduced quite a few other classes for manipulating various aspects of date and time—see Chapter 6 of Volume II.

Separating the time measurement from calendars is good object-oriented design. In general, it is a good idea to use different classes to express different concepts.

You do not use a constructor to construct objects of the `LocalDate` class. Instead, use static *factory methods* that call constructors on your behalf. The expression

```java
LocalDate.now()
```

constructs a new object that represents the date at which the object was constructed.

You can construct an object for a specific date by supplying year, month, and day:

```java
LocalDate.of(1999, 12, 31)
```

### 4.2.3 Mutator and Accessor Methods

Have another look at the plusDays method call that you saw in the preceding section:

```java
LocalDate aThousandDaysLater = newYearEve.plusDays(1000);
```

What happens to newYearEve after the call? Has it been changed to be a thousand days later? As it turns out, it has not. The plusDays method yields a new LocalDate object, which is then assigned to the aThousandDaysLater variable. The original object remains unchanged. Say that the plusDays method does not mutate the object on which it is invoked. (This is similar to the toUpperCase method of the String class that you saw in Chapter 3. When you call toUpperCase on a string, that string stays the same, and a new string with uppercase characters is returned.)

An earlier version of the Java library had a different class for dealing with calendars, called GregorianCalendar. Here is how you add a thousand days to a date represented by that class:

```java
GregorianCalendar someDay = new GregorianCalendar(1999, 11, 31);
   // add 1000 days to that date; month numbers go from 0 to 11
   someDay.add(Calendar.DAY_OF_MONTH, 1000);
```

Unlike the LocalDate.plusDays method, the GregorianCalendar.add method is a mutator method. After invoking it, the state of the someDay object has changed. Here is how you can find out the new state:

```java
year = someDay.get(Calendar.YEAR); // 2002
month = someDay.get(Calendar.MONTH) + 1; // 09
day = someDay.get(Calendar.DAY_OF_MONTH); // 26
```

That’s why we called the variable someDay and not newYearEve—it no longer is new year’s eve after calling the mutator method.

In contrast, methods that only access objects without modifying them are sometimes called accessor methods. For example, LocalDate.getYear and GregorianCalendar.get are accessor methods.

![](img/127bccebb2cfadea3f02579edaad63c3_164_0.png)

> **C++ NOTE:** In C++, the const suffix denotes accessor methods. A method that is not declared as const is assumed to be a mutator. However, in the Java programming language, no special syntax distinguishes accessors from mutators.

We finish this section with a program that puts the LocalDate class to work. The program displays a calendar for the current month, like this:

![](img/127bccebb2cfadea3f02579edaad63c3_165_0.png)

The current day is marked with an asterisk (*). As you can see, the program needs to know how to compute the length of a month and the weekday of a given day.

Let us go through the key steps of the program. First, we construct an object that is initialized with the current date.

```java
LocalDate date = LocalDate.now();
```

We capture the current month and day.

```java
int month = date.getMonthValue();
int today = date.getDayOfMonth();
```

Then we set date to the first of the month and get the weekday of that date.

```java
date = date.minusDays(today - 1); // set to start of month
DayOfWeek weekday = date.getDayOfWeek();
int value = weekday.getValue(); // 1 = Monday, . . . , 7 = Sunday
```

The variable weekday is set to an object of type DayOfWeek. We call the getValue method of that object to get a numerical value for the weekday. This yields an integer that follows the international convention where the weekend comes at the end of the week, returning 1 for Monday, 2 for Tuesday, and so on. Sunday has value 7.

Note that the first line of the calendar is indented, so that the first day of the month falls on the appropriate weekday. Here is the code to print the header and the indentation for the first line:

```java
System.out.println("Mon Tue Wed Thu Fri Sat Sun");
for (int i = 1; i < value; i++)
    System.out.print("   ");
```

Now, we are ready to print the body of the calendar. We enter a loop in which date traverses the days of the month.

In each iteration, we print the date value. If date is today, the date is marked with an *. Then, we advance date to the next day. When we reach the beginning of each new week, we print a new line:
