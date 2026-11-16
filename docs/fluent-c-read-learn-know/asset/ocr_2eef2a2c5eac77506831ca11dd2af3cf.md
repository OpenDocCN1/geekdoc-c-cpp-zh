# ...ANCIENT DAYS

Even in the current era in Europe, you can run into calendar issues when working with history. The Gregorian calendar was first proposed in 1582, but not fully adopted until it was finally adopted by Greece in 1923. Because of the change from the Julian to the Gregorian calendar, certain dates simply never occurred in the adopting countries. October 21, 1582, is a valid date in The Netherlands, for example, but not in Spain. The .NET Framework representation of dates (even in the DateTimeOffset structure) simply isn't sophisticated enough to deal with these issues.

Be aware, too, that programmers tend to use the word “Julian” incorrectly to refer to a format rather than a date. When you hear someone talking about “Julian dates,” they almost certainly mean a date in the month, day, year format common in the United States (July 4, 1776 as opposed to 4 July, 1776).

![](bbox=[0.11, 0.43, 0.21, 0.58])

# PUT ON YOUR THINKING HAT

Assuming a variable called Date1 initialized to January 1, 2010, can you write the statements to perform the following operations? As always, you can use the Object Browser to explore what DateTime knows and does, and press F1 on a specific member to get more details.

+   Set Date1 to the current operating system date, ignoring the time.

+   Add 3 days to the value of Date1.

+   Display the name of the day of the week in a MessageBox. (Hint: Use the static Enum.GetName() method to retrieve the string representation of the DayOfWeek enumeration.)

+   In a MessageBox, display the number of days in the month contained in Date1.

+   Determine whether Date1 is earlier than the current operating system date.