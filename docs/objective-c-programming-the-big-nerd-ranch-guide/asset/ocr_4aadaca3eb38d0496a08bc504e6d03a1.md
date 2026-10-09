# # 15
# NSArray

Like **NSS**tring, **NSArray** is another class that Objective-C programmers use a lot. An instance of **NSArray** holds a list of pointers to other objects. For example, let's say you want to make a list of three NSDate objects and then go through the list and print each date.

Create a new project : a Foundation Command Line Tool called DateList. Open main.m and change the **main()** function:

```
```
#import <Foundation/Foundation.h>
int main(int argc, const char * argv[])
{
@autoreleasepool {

// Create three NSDate objects
NSDate *now = [NSDate date];
NSDate *tomorrow = [now dateByAddingTimeInterval:24.0 * 60.0 * 60.0];
NSDate *yesterday = [now dateByAddingTimeInterval:-24.0 * 60.0 * 60.0];

// Create an array containing all three (nil terminates the list)
NSArray *dateList = [NSArray arrayWithObjects:now, tomorrow, yesterday, nil];

// How many dates are there?
NSLog(@"There are %lu dates", [dateList count]);

// Print a couple
NSLog(@"The first date is %@", [dateList objectAtIndex:0]);
NSLog(@"The third date is %@", [dateList objectAtIndex:2]);
}
return 0;
}
```
```

**NSArray** has two methods, shown in this example, that you will use all the time:

+   * **count** returns the number of items in an array

+   * **objectAtIndex:** returns the pointer that the array has stored at the index specified by the argument.

Arrays are ordered, and you access an item in the array by its *index*. Arrays are zero-based: the first item is stored at index 0, the second item is stored at index 1, and so on. Thus, if the **count** method says there are 100 items in the array, you can use **objectAtIndex:** to ask for the objects at indices 0 to 99.