```
```java
String message = String.format("Hello, %s. Next year, you'll be %d", name, age);
```
```

In the interest of completeness, we briefly discuss the date and time formatting options of the printf method. For new code, you should use the methods of the java.time package described in Chapter 6 of Volume II. But you may encounter the Date class and the associated formatting options in legacy code. The format consists of two letters, starting with t and ending in one of the letters of Table 3.7; for example,

```
```java
System.out.printf("%tc", new Date());
```
```

prints the current date and time in the format

```
```
Mon Feb 09 18:05:19 PST 2015
```
```

# **Table 3.7** Date and Time Conversion Characters

| Conversion Character | Type | Example |
|---|---|---|
| c | Complete date and time | Mon Feb 09 18:05:19 PST 2015 |
| F | ISO 8601 date | 2015-02-09 |
| D | U.S. formatted date (month/day/year) | 02/09/2015 |
| T | 24-hour time | 18:05:19 |
| r | 12-hour time | 06:05:19 pm |
| R | 24-hour time, no seconds | 18:05 |
| Y | Four-digit year (with leading zeroes) | 2015 |
| y | Last two digits of the year (with leading zeroes) | 15 |
| C | First two digits of the year (with leading zeroes) | 20 |
| B | Full month name | February |
| b or h | Abbreviated month name | Feb |
| m | Two-digit month (with leading zeroes) | 02 |
| d | Two-digit day (with leading zeroes) | 09 |
| e | Two-digit day (without leading zeroes) | 9 |
| A | Full weekday name | Monday |

*(Continues)*