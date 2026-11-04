
| CHARACTER | MEANING | EXAMPLE |
| --- | --- | --- |
| U | Universal sortable full date/time | Thursday, April 5, 2063 7:23:45 PM |
| Y or y | Year month | April, 2063 |

> **NOTE** The result given by the U format may seem a bit surprising because it gives the time as 7:23:45 PM instead of 1:23:45 PM. The reason is the U specifier automatically converts a local time into Coordinated Universal Time (UTC) before formatting. (UTC is the time at 0° longitude. It’s basically the same as Greenwich Mean Time or GMT.) On April 5, 2063, the time 1:23 PM in my time zone will be 7:23 PM in Greenwich.

The DateTime class also provides several methods that return the date’s value as a string formatted in the most common date and time formats. Table 14-6 summarizes the most useful of these methods and shows the results on my computer set up for US English. Your results will depend on how your computer is configured.

**TABLE 14-6**

| METHOD | FORMAT | EXAMPLE |
| --- | --- | --- |
| ToLongDateString | Long date (D) | Thursday, April 5, 2063 |
| ToLongTimeString | Long time (T) | 1:23:45 PM |
| ToShortDateString | Short date (d) | 4/5/2063 |
| ToShortTimeString | Short time (t) | 1:23 PM |
| ToString | General date and time (g) | 4/5/2063 1:23:45 PM |

> **NOTE** As is the case with number formats, you should use the standard specifiers or the standard methods (such as ToLongDateString) whenever possible so your computer can display dates and times in the formats used by the computer’s locale.

## Custom Date and Time Formats

If the standard date and time formatting characters don’t do the trick, you can use a custom format. Table 14-7 summarizes the custom date and time formatting strings. Note that for many of the characters in this table, the uppercase and lowercase versions have different meanings.

**TABLE 14-7**

| CHARACTER | MEANING |
| --- | --- |
| d | Day of month between 1 and 31. |
| dd | Day of month between 01 and 31. |
| ddd | Abbreviated day of week (Mon, Tue, and so on). |
| dddd | Full day of week (Monday, Tuesday, and so on). |
| f | Digits after the decimal for seconds. For example, ffff means use four digits. |
| F | Similar to f but trailing zeros are not displayed. |
| g | Era specifier. For example, A.D. |
| h | Hours between 1 and 12. |
| hh | Hours between 01 and 12. |
| H | Hours between 0 and 23. |
| HH | Hours between 00 and 23. |
| m | Minutes between 1 and 59. |
| mm | Minutes between 01 and 59. |
| M | Month between 1 and 12. |
| MM | Month between 01 and 12. |
| MMM | Month abbreviation (Jan, Feb, and so on). |
| MMMM | Month name (January, February, and so on). |
| s | Seconds between 1 and 59. |
| ss | Seconds between 01 and 59. |
| t | First character of AM/PM designator. |
| tt | AM/PM designator. |
| y | One- or two-digit year. If the year has fewer than two digits, it is not zero padded. |
| yy | Two-digit year, zero padded if necessary. |
| yyy | Three-digit year, zero padded if necessary. |
| yyyy | Four-digit year, zero padded if necessary. |
| yyyyy | Five-digit year, zero padded if necessary. |
| z | Signed time zone offset from UTC. |
| zz | Signed time zone offset from UTC in two digits. |
| zzz | Signed time zone offset from UTC in hours and minutes. |
| : | Hours, minutes, and seconds separator. |
| / | Date separator. |
| 'ABC' | Literal string. Characters enclosed in single or double quotes are displayed without any conversion. |

> **NOTE** The time zone offset values depend on whether daylight savings is in effect. For example, for Pacific Standard Time the zzz specifier returns either –08:00 or –07:00 depending on whether daylight savings is in effect on that date.

> **NOTE** The date and time formatting methods assume that a single character is a standard format. For example, the `date.ToString("d")` would give you a short date format, not the day of the month.
>
> When a single character specifier is inside a longer string, the formatting methods treat it like a custom specifier. For example, `date.ToString("M/d")` gets you the month and day numbers.
>
> If you need to use a custom specifier alone, place a `%` symbol in front of it. For example, `date.ToString("%d")` returns the day number by itself.

Table 14-8 shows some example formats and their results. The date used was 1:23:45.678 PM April 5, 2063 on my computer set up for US English. Your results will depend on how your computer is configured.

**TABLE 14-8**

| FORMAT | RESULT |
| --- | --- |
| M/d/yy | 4/5/63 |
| d MMM yy | 5 Apr 63 |
| HH:mm 'hours' | 13:23 hours |

- 6. [Hard] Copy the program that you built for Exercise 1 and modify it so the main form displays items in a ListBox instead of a ListView. Make the program use string.Format to add items to the ListBox in a format similar to the following:

  Hint: When you remove an item from the list, you need to subtract its total cost from the grand total. Use the item’s ToString method to convert it into a string. Then use the methods you used for Exercise 5 to parse the string and find the item’s total cost.

  ```
  1,200 Gummy bugs at $0.02 each = $24.00
  ```

- 7. Make a program that replaces all occurrences of the letter E (uppercase and lowercase) in a string entered by the user with the character -.

- 8. Make a program that lets the user enter an input string, a string to replace, and a replacement string. When the user clicks the Replace button, make the replacement and display the result in the same TextBox as the original string so the user can make several replacements easily. To make using the program even easier, also make the button clear the string to replace and the replacement string and set focus to the string to replace.

- 9. Write a program that lets the user enter a string such as, “The 6th sheik’s 6th sheep’s sick.” When the user clicks the Replace button, replace numerals with their spelled out equivalents as in, “The sixth sheik’s sixth sheep’s sick.” Don’t worry about punctuation (like capitalizing if the sentence begins with a numeral), numbers bigger than 9 (so “10” will become “onezero”), or special cases (like converting 3rd into third). (Then try to say “The sixth sheik’s sixth sheep’s sick” as quickly as you can.)

- 10. Write a program that lets the user enter a number. When the user clicks the Format button, use a custom format specifier with three sections to format the number. If the number is positive, display it as in +1,234.56 (two digits after the decimal point). If the number is negative, display it as in -1,234.56 (again two digits after the decimal point). If the number is zero, display ZERO.

> **NOTE** Please select the videos for Lesson 14 online at www.wrox.com/go/csharp24hourtrainer2videos.

**TABLE 15-1**

| METHOD | PURPOSE |
| --- | --- |
| Add | Adds a TimeSpan to the DateTime. The following section describes TimeSpan. |
| AddDays | Adds a specified number of days to the DateTime. |
| AddHours | Adds a specified number of hours to the DateTime. |
| AddMinutes | Adds a specified number of minutes to the DateTime. |
| AddMonths | Adds a specified number of months to the DateTime. |
| AddSeconds | Adds a specified number of seconds to the DateTime. |
| AddYears | Adds a specified number of years to the DateTime. |
| IsDaylightSavingTime | Returns true if the date and time is within the Daylight Saving Time period for the local time zone. |
| IsLeapYear* | Returns true if the indicated year is a leap year. |
| Parse* | Parses a string and returns the corresponding DateTime. |
| Subtract | Subtracts another DateTime from this one and returns a TimeSpan. The following section says more about TimeSpan. |
| ToLocalTime | Converts the DateTime to a local value. |
| ToLongDateString | Returns the DateTime in long date format. |
| ToLongTimeString | Returns the DateTime in long time format. |
| ToShortDateString | Returns the DateTime in short date format. |
| ToShortTimeString | Returns the DateTime in short time format. |
| ToString | Returns the DateTime in general format. |
| ToUniversalTime | Converts the DateTime to a UTC value. |

Table 15-2 summarizes the DateTime’s most useful properties.

**TABLE 15-2**

| PROPERTY | PURPOSE |
| --- | --- |
| Date | Gets the DateTime’s date without the time. |
| Day | Gets the DateTime’s day of the month between 1 and 31. |
| DayOfWeek | Gets the DateTime’s day of the week, as in Monday. |
