# Listing 15.4

# Comparing dates

```
NSDate *now = [NSDate date];
NSDate *anHourAgo = [now dateByAddingTimeInterval:-3600];
assert([now laterDate:anHourAgo] == now); // true
assert([now earlierDate:anHourAgo] == anHourAgo); // true
assert([now compare:anHourAgo] == NSOrderedDescending); // true
```

# Using NSCalendar

Although it can be useful to construct an NSDate for a specific instant in time using an NSTime Interval, more often you will want to construct an NSDate for a specific day or a relative time based on calendar representations of time rather than the number of seconds. Not only is this easier to think of conceptually, it is also often more accurate and less prone to error. These are the cases where the edge conditions in calendar manipulation are most likely to bite you.

The Foundation framework provides the NSCalendar class for exactly this purpose. It provides a mechanism for specifying dates using more natural date components, such as day, month, week, and so on. It does this not only for the Gregorian calendar as we use it today, but also for specialized calendars, such as Hebrew calendars, Islamic calendars, Buddhist calendars, and so on. In this way, it also provides a powerful localization tool for delivering a rich localized experience for your users.

To construct a new NSDate object for a given day of a given month, you first construct an NSDateComponents object, and use it to set whatever parameters you want to include. You then construct an NSCalendar for the calendar in which you are trying to construct the date. Using these two together, you can then create the NSDate object representing the day you’re looking for. Listing 15.5 shows how to do this.

# Listing 15.5

# Constructing an NSDate using NSDateComponents and NSCalendar

```
NSDateComponents *components = [[NSDateComponents alloc] init];
[components setMonth:4];
[components setDay:13];
[components setYear:2010];

NSCalendar *currentCalendar = [NSCalendar currentCalendar];
NSDate *date = [currentCalendar dateFromComponents]; // 04/13/2010
```