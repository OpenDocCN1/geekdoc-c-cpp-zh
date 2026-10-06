
```c
struct CGRect {
    CGPoint origin;
    CGSize size;
};
typedef struct CGRect CGRect;
```

The typedefs provide a convenient way to declare variables without having to use the keyword struct. CGFloat is just a typedef for a basic float type. So you want to declare a CGPoint variable and set its x member to 100 and y member to 200, respectively, you could write this code sequence:

```
CGPoint startPt;

startPt.x = 100;
startPt.y = 200;
```

Remember startPt is a structure and not an object. (A good indication of that is often the lack of an asterisk in front of the variable name.) Apple also provides convenience functions for creating CGRect, CGSize, and CGRect structures. For example,

```
CGPoint startPt = CGPointMake(100.0, 200.0);
```

There's also CGSizeMake and CGRect functions that perform tasks as their names imply.

So let's say you want to define a new rectangle and set its size to 200 x 100. You could specify its size this way:

```
CGSize rectSize;
```

```
rectSize.width = 200;
rectSize.height = 100;
```

or your could use the CGSizeMake function like so:

```
CGSize rectSize = CGSizeMake (200.0, 100.0);
```

Now let's go ahead and create a rectangle with the indicated size and origin:

```
CGRect theFrame;
```

```
theFrame.origin = startPt;
theFrame.size = rectSize;
```

(We won't show the use of the CGRectMake function here.)

Suppose later you want to get the rectangle's width (maybe changed?). You could do so by writing this expression:

```
theFrame.size.width
```

And to change its width to 175, you could write this:

```
theFrame.size.width = 175;
```

Finally, to set the rectangle's origin to (0,0), these statements would do the trick:

```
theFrame.origin.x = 0.0;
theFrame.origin.y = 0.0;
```

These are just a few examples of working with these structures. As noted, you'll likely be using them often in your applications.

## Additional Details About Structures

We should mention that you have some flexibility in defining a structure. First, you can declare a variable to be of a particular structure type at the same time that the structure is defined. You do this simply by including the variable name(s) before the terminating semicolon of the structure definition. For example, the following statement defines the structure date and also declares the variables todaysDate and purchaseDate to be of this type:

```
struct date
  int month;
  int day;
  int year;
} todaysDate, purchaseDate;
```

You can assign initial values to the variables in the normal fashion. Thus, the following defines the structure date and the variable todaysDate with initial values as indicated:

```
struct date
  int month;
  int day;
  int year;
} todaysDate = { 9, 25, 2011 } ;
```

If all the variables of a particular structure type are defined when the structure is defined, you can omit the structure name. So the following statement defines an array called dates to consist of 100 elements:

```
struct
  int month;
  int day;
  int year;
} dates[100];
```

Each element is a structure containing three integer members: month, day, and year. Because you did not supply a name to the structure, the only way to subsequently declare variables of the same type is to explicitly define the structure again.

## Don’t Forget About Object-Oriented Programming!

Now you know how to define a structure to store a date, and you've written various routines to manipulate that date structure. But what about object-oriented programming? Shouldn't you have made a class Date instead and then developed methods to work with a Date object? Wouldn't that be a better approach? Well, yes. Hopefully, that entered your mind when we were discussing dates in your program.

Certainly, if you have to work with a lot of dates in your programs, defining a class and methods to work with dates is a better approach. In fact, the Foundation framework has a couple of classes, called NSDate and NSCalendarDate, defined for such purposes. We leave it as an exercise for you to implement a Date class to deal with dates as objects instead of structures.

## Pointers

Pointers enable you to effectively represent complex data structures, change values passed as arguments to functions and methods, and more concisely and efficiently deal with arrays. At the end of this chapter, we also clue you in about how important they are to the implementation of objects in the Objective-C language.

We introduced the concept of a pointer in Chapter 8, "Inheritance," when we talked about the Point and Rectangle classes and stated that you can have multiple references to the same object.

To understand the way pointers operate, you must first understand the concept of indirection. We witness this concept in our everyday life. For example, suppose that I needed to buy a new toner cartridge for my printer. In the company that I work for, the purchasing department handles all purchases. So I would call Jim in purchasing and ask him to order the new cartridge for me. Jim would then call the local supply store to order the cartridge. To obtain my new cartridge, I would take an indirect approach because I would not be ordering the cartridge directly from the supply store.

This same notion of indirection applies to the way pointers work in Objective-C. A pointer provides an indirect means of accessing the value of a particular data item. And just as there are reasons it makes sense to go through the purchasing department to order new cartridges (I don't have to know which particular store the cartridges are being ordered from, for example), good reasons exist for why sometimes it makes sense to use pointers in Objective-C.

But enough talk; it's time to see how pointers actually work. Suppose you've defined a variable count as follows:

```
int count = 10;
```

You can define another variable, called intPtr, that enables you to indirectly access the value of count with the following declaration:

```
int *intPtr;
```

The asterisk defines the Objective-C system that the variable intPtr is of type pointer to int. This means that the program will use intPtr to indirectly access the value of one or more integer variables.

You have seen how we used the & operator in the scanf calls of previous programs. This unary operator, known as the address operator, makes a pointer to a variable in Objective-C. So if x is a variable of a particular type, the expression &x is a pointer to that variable. If you want, you can assign the expression &x to any pointer variable that has been declared to be a pointer of the same type as x.

Therefore, with the definitions of count and intPtr as given, we can write a statement such as

```
intPtr = &count;
```

to set up the indirect reference between intPtr and count. The address operator assigns to the variable intPtr not the value of count, but a pointer to the variable count. Figure 13.1 illustrates the link made between intPtr and count. The directed line illustrates the idea that intPtr does not directly contain the value of count, but contains a pointer to the variable count.

## Figure 13.1. Pointer to an integer

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_432_0.png)

To reference the contents of count through the pointer variable intPtr, you use the indirection operator, which is the asterisk (*). If x were defined to be type int, the statement

```
x = *intPtr;
```

would assign the value that is indirectly referred through intPtr to the variable x. Because intPtr was previously set pointing to count, this statement would have the effect of assigning the value contained in count—which is 10—to the variable x.

Program 13.11 incorporates the previous statements and the two fundamental pointer operators: the address operator (&) and the indirection operator (*).

# Program 13.11

```
// Program to illustrate pointers

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int count = 10, x;
        int *intPtr;

        intPtr = &count;
        x = *intPtr;

        NSLog("count = %i, x = %i", count, x);
    }
    return 0;
}
```

# Program 13.11. Output

count = 10, x = 10

The variables count and x are declared to be integer variables in the normal fashion. On the next line, the variable intPtr is declared to be of type "pointer to int." Note that the two lines of declarations could have been combined into a single line:

```
int count = 10, x, *intPtr;
```

Next, the address operator is applied to the variable count, which has the effect of creating a pointer to this variable, which the program then assigns to the variable intPtr.

Execution of the next statement in the program
