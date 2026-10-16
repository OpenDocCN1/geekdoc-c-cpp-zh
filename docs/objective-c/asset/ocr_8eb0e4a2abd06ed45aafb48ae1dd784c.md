# Listing 15.2

# Creating dates with time intervals

```
NSDate *now = [NSDate date];
NSDate *anHourAgo = [now dateByAddingTimeInterval:-3600];
NSDate *anHourFromNow = [now dateByAddingTimeInterval:3600];
```

# Comparing dates

You can compare dates to determine whether one or the other is earlier, later, equal, or to determine how much of a time interval exists between two dates.

To find out the time interval between two dates, you use the method -timeIntervalSinceDate:. You call this method on one of your dates, passing another day as the parameter. This method returns the time interval between the two dates. Just like when constructing a new NSDate object, the NSTimeInterval that is returned will be positive if the receiver of the call is after the given parameter and negative if the receiver is before the parameter. There is also the shortcut method -timeIntervalSinceNow, which simply gives you the time interval between the receiver and the current time. Listing 15.3 shows some examples of these methods in use.

# Listing 15.3

# Calculating the time interval between different dates

```
NSDate *now = [NSDate date];
NSDate *anHourAgo = [now dateByAddingTimeInterval:-3600];
NSTimeInterval timeBetween = [now timeIntervalSinceDate:anHourAgo]; // 3600
```

Additionally, the NSDate class also provides the methods -laterDate:, -earlierDate:, and compare: for the purposes of comparing dates. In the case of the methods -laterDate: and -earlierDate:, these methods return the later or earlier, respectively, date of the two dates being compared. Meanwhile, the -compare: method returns a standard NSComparisonResult, and is useful when sorting dates. Listing 15.4 shows these methods in action.