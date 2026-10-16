
The word `typedef` comes from the words *type definition*, and essentially allows you to define your own types. Using it in conjunction with structures enables you to define a custom type that represents your structure. You can then use this custom type anywhere you’d normally have used your structure definition. Listing 2.13 shows the `typedef` version of the `Point` structure example.

## Listing 2.13
### Working with point structures and typedefs

```
#import <Foundation/Foundation.h>

// declaring the point structure.
typedef struct
{
    float x;
    float y;
} Point;

int main(int argc, const char *argv[])
{
    // declaring the point variable...
    Point p;
    // assigning values to the struct's members...
    p.x = 20.0;
    p.y = 50.0;

    // ... then to use the point...
    moveCursorToPoint(p);

    return 0;
}
```

As you can see, by simply adding the `typedef` keyword before the `struct` keyword, and by moving the `struct` name to the end of the structure, it does something amazing; it allows you to declare your p variable by simply doing Point p. Essentially, Point becomes a first-class type, and you can use it anywhere you would be using any other type.

The syntax to use the `typedef` keyword consists of `typedef variable-definition new-type-name`. Where `variable-definition` is the actual type you want inserted when you use the new type, and `new-type-name` is the new type name that you will use in your program.

Due to the way typedefs allow you to use type names that more clearly describe the type of data that will be stored in a variable, typedefs are a nice addition that makes your code more self-documenting than code that doesn’t use them. I touch on using typedefs again in Chapter 5 when I discuss using blocks.

## Using enum

Another way to define a custom datatype is to use the enum keyword. Enum is short for enumerated type, and it allows you to create a datatype, which has a restricted list of possible values that can be stored in it. Enums are often used in Cocoa and Cocoa Touch for parameters and return values where the list of possible values falls within a specific limited set.

To define an enum, you use the enum keyword, followed by a tag for the enum you are declaring, then followed by {}, which contain a list of the possible values for the enum separated by commas. Listing 2.14 shows an enum definition.

## Listing 2.14
### Creating an enum

```
enum MyEnum
{
    Value1,
    Value2,
    Value2
};
```

To use an enum in your code, you must declare a variable to be of type enum, followed by the tag that you specified when defining your enum. Then, to assign a value to it, you simply use one of the allowed values from your enum definition. Listing 2.15 shows how this is done.

## Listing 2.15
### Using an enum

```
enum MyEnum foo;
foo = Value1;

// or for a function
enum MyEnum myFunction();

// as a parameter to a function
void myFunction(enum MyEnum foo);
```

The actual values of the enums themselves are determined by the compiler, but they default to integers, starting at 0 for the first value, 1 for the second, and so on. You can force an enum to assign a specific value to one of the values by simply providing that value as part of the enum definition, as shown in Listing 2.16.

## Listing 2.16
### Assigning values to the enum options

```
enum MyEnum
{
    Value1 = 20,
    Value2 = 13,
    Value3 = 155
};
```

This can be useful when dealing with legacy code that expects a specific value.

Typing out enum whenever you use an enum can be inconvenient. So enums can be typedef’d just like structures can. Listing 2.17 shows how this works.

## Listing 2.17
### Using typedef with an enum

```
enum MyEnumType
{
    Value1,
    Value2,
    Value3
};
typedef enum MyEnumType MyEnum;

// Now this allows you to type...
MyEnum foo;
foo = Value1;
```

Cocoa and Cocoa Touch use enums quite a bit. The nice thing about enums is that they allow you to have a compile-time check to verify that the parameter passed to your function is one of a limited set of values. If you accidentally pass the wrong value, the compiler will generate an error.

## Understanding pointers

The third type of variable I'm going to discuss are pointers. Pointers can be a difficult concept to wrap your head around, but fortunately, in Objective-C, the more complex aspects of pointers are rarely used. However, understanding them is important.

Recall that a typical variable stores data in RAM. The computer looks up the variable by using an address in RAM. Metaphorically speaking, if you can imagine a variable as being a house where people (data) live, the street address of the house is the address of that variable.

A pointer is a variable that contains the address of another variable. Declaring a pointer is similar to declaring a variable of whatever type it is that you want to point to except that you also include the pointer operator as part of your declaration. The pointer operator is an asterisk (*). You can get the address of a variable by using the address-of operator (&).

Listing 2.18 shows an example of declaring a pointer to an integer.

## Listing 2.18
### Declaring pointers

```
#import <Foundation/Foundation.h>

int main(int argc, char *argv[])
{
    int x = 5;
    int *y = &x;

    NSLog(@"X:%ld - Y:%ld", x, y);
    return 0;
}
```

In this code, you are declaring a variable, x, which is an int. Within this variable, you are storing the value of 5. We are then declaring another variable, y, which is of type pointer to an int, and within it, we are storing the address of x.

Pointers can be used just like regular variables, but when you access them directly, such as what we are doing on line 8 of this program, the value you get is a memory address. In this case, when you run this program, you should see output, as shown in Figure 2.2.

Your value for y will probably vary from mine because your computer may be storing your x value at a different address from mine. This is normal. The asterisk operator (*) is also the pointer-dereferencing operator. The process of dereferencing a pointer allows you to access the value of the variable that the pointer points to. So in other words, in your program example, you want to print the value that the white pointer was pointing to, in other words the value of x, then you could rewrite your program to look like Listing 2.19.

## Figure 2.2
Output of the pointer program

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_64_0.png)

## Listing 2.19
### Dereferencing pointers

```
#import <Foundation/Foundation.h>

int main(int argc, char *argv[])
{
    int x = 5;
    int *y = &x;

    NSLog(@"X:%ld - Y:%ld", x, *y);
    return 0;
}
```

Notice that we are now dereferencing y, which means that when you run this application, you should see something like Figure 2.3.

## Figure 2.3
Output of the dereferencing example code

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_65_0.png)

The interesting thing about pointers is that they can be manipulated just like regular variables. This means that you can increment them, you can decrement them, you can add to them, and you can subtract from them. You can do all these things, but what you’re really doing is changing the location in RAM where the pointer is pointing. Consequently, you can then dereference the pointer at the new location and access a different value than where it was originally pointing.

Most of this discussion of pointers is relatively advanced subject matter. In day-to-day Objective-C, you typically don’t have the need to dereference many pointers. (There are a couple exceptions to this rule, and I will point them out as we go through this book.) For a deeper understanding of low-level pointers, I suggest picking up a good book on the C programming language.

Typical Objective-C use of pointers is primarily limited to the declaration of objects. Objects in Objective-C are in fact pointers. Fortunately, for the most part, even though they are pointers, you rarely have to think of them in that way. The most important thing that you do need to remember is that anytime you are declaring an object, it needs to be declared as a pointer. For example, look at Listing 2.20.
