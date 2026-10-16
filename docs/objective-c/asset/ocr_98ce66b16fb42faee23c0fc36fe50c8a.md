zone in a given address calendar object. Just like specifying different calendar types, the time zone of the given NSCalendar can affect the calculated time of a given instant compared to the same time in another region. In other words, this moment in time one week ago in a different time zone would actually be a different time in terms of hours than the same time in your current time zone.

NSTimeZone also provides a list of all the time zones it knows about by using the class method +knownTimeZoneNames. You can use this class method to present a list of time zones to the user.

You create an NSTimeZone object by specifying the time zone name as a parameter to the factory method +timeZoneWithName: or by specifying the abbreviation of that time zone by using the factory method +timeZoneWithAbbreviation:. These are shown in Listing 15.8.

# Listing 15.8

# Creating NSTimeZone objects

```
NSTimeZone *est = [NSTimeZone timeZoneWithAbbreviation:@"PST"];

NSTimeZone *azZone = [NSTimeZone timeZoneWithName:@"America/Arizona/Phoenix"];
```

After you have constructed these objects, you can use them in conjunction with your NSCalendar object. If you do not explicitly set the time zone on your calendar, it uses the system's default time zone. But if you want your times to be in a particular time zone, you can set the time zone on the NSCalendar, and then any dates you get from that calendar will be adjusted accordingly.

# Using NSDateFormatter

Most of the time, when working with dates, you wind up representing those dates to the user as a string. Just like when working with dates themselves, numerous edge conditions need to be accounted for when doing date to string conversions. Aside from simple standard localization issues, such as getting the month and day names correct for the users region, consider that there are different formats at different dates can be represented using. For example, a day of the week can be represented as its full name, Tuesday, as an abbreviated version, Tue, or just a letter T. Months are even more complicated. They can be represented as a full name, September, an abbreviation, Sept. or a number, 9. In the U.S. dates are typically represented as MM/DD/YYYY, whereas in Europe, they are represented as DD/MM/YYYY. As you can see, the potential variations are infinite.