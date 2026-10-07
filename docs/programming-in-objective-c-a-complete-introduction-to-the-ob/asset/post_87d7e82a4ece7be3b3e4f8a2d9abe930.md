
# Pointers

Pointers enable you to effectively represent complex data structures, change values passed as arguments to methods, and more concisely and efficiently deal with arrays. At the end of this chapter, we also give clue about how important they are to the implementation of objects in the Objective-C language.

We introduced the concept of a pointer in Chapter 8, "Inheritance," when we talked about the Point and Rectangle classes and stated that you can have multiple references to the same object.

To understand how pointers operate, you must first understand the concept of indirection. We witness this concept in our everyday life. For example, suppose that I needed to buy a new toner for my printer. In the company that I work for, the purchasing department handles all purchases. So I would call Jim in purchasing and ask him to order the new cartridge for me. Jim then would call the local supply store to order the cartridge. To obtain my new cartridge, I would take an indirect approach because I would

This same notion of indirection applies to the way pointers work in Objective-C. A pointer provides an indirect means of accessing the value of a particular data item. And just as there are reasons it makes sense to go through the purchasing department to order new cartridges (I don't know which particular cartridges are being ordered from, for example), good reasons exist why sometimes it makes sense to use pointers in Objective-C.

But enough talk; it's time to see how pointers actually work. Suppose you've defined a variable count as follows:

```
int count = 10;
```

You can define another variable, int intPtr, that enables you to indirectly access the value of count with the following declaration:

```
int *intPtr;
```

The asterisk indicates the Objective-C system that the variable intPtr is of type pointer to int. This means that the program will use intPtr to access the value of one or more integer variables.

You have seen how the & operator in the scanf calls of previous programs. This unary operator, known as the address operator, makes a pointer to a variable in Objective-C. So if x is a variable of a particular type, the expression &x is a pointer to that variable. If you want, you can assign the expression &x to any pointer variable that has been declared to be a pointer of the same type as x.

Therefore, with the definitions of count and intPtr as given, you can write a statement as

```
intPtr = &count;
```

to set up the indirect reference between intPtr and count. The address operator assigns to the variable intPtr not the value of count, but a pointer to the variable count.

Figure 13.1 illustrates the link between intPtr and count. The directed line illustrates the idea that intPtr does not directly contain the value of count, but contains a pointer to the variable count.

![](img/9a03a17dbf1900dce936c9665ab15c26_287_0.png)

Figure 13.1 Pointer to an integer

To reference the contents of count through the pointer variable intPtr, you use the indirection operator, which is the asterisk (*). If x were to be defined of type int, the statement x = *intPtr; would assign the value that is indirectly referenced through intPtr to the variable x. Because intPtr was previously set pointing to count, this statement would have the effect of assigning the value contained in the variable count—which is 10—to the variable x. Program 13.11 incorporates the previous statements and illustrates the two fundamental pointers: the address operator (&) and the indirection operator (*).

# Program 13.11

```
// Program to illustrate pointers

#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc init];
    int count = 10, x;
    int *intPtr;

    intPtr = &count;
    x = *intPtr;

    NSLog("@count = %i, x = %i", count, x);

    [pool drain]
    return 0;
}
```

# Program 13.11 Output

count = 10, x = 10

The variables count and x are declared to be integer variables in the normal fashion. On the next line, the variable intPtr is declared to be of type "pointer to int." Note that the two lines of declarations could have been combined into a single line:

```
int count = 10, x, *intPtr;
```

# 276 Chapter 13 Underlying C Language Features

Next, the address operator is applied to the variable count, which has the effect of creating a pointer to this variable, which the program assigns to the variable intPtr. Execution of the next statement in the program

```
x = *intPtr;
```

proceeds as follows: The indirection operator tells the Objective-C system to treat the variable intPtr as containing a pointer to another data item. This pointer is then used to access the desired item, whose type is specified by the declaration of the pointer variable. Because you told the compiler when you declared the variable intPtr points to integers, the compiler knows that the value referenced by the expression *intPtr is an integer. Also, because you set intPtr to point to the integer variable count in the previous statement, this expression directly accesses the value of count.

Program 13.12 illustrates some interesting properties of pointer variables. This program uses a pointer to a character.

# Program 13.12

```
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    NSautoreleasePool *pool = [[NSautorelease alloc] init];
    char *c = 'Q';
    char *charPtr = &c;

    NSLog("%@c %c", c, *charPtr);
    c = '/';
    NSLog("%@c %c", c, *charPtr);

    *charPtr = '(';
    NSLog("%@c %c", c, *charPtr);

    [pool drain];
    return 0;
}
```

# Program 13.12 Output

Q Q
/\(

The character variable c is defined and initialized to the character 'Q'. In the next line of the program, the variable charPtr is defined to be of type "pointer to char," meaning that whatever value is stored inside this variable should be treated as an indirect reference (pointer) to a character. Notice that you can assign an initial value to this variable in the normal fashion. The value you assign to charPtr in the program is a pointer to the variable c, which is obtained by applying the address operator to the variable c. (Note that this initialization would have generated a compiler error had c been defined after this statement because a variable must always be declared before its value be referenced in an expression.)

The declaration of the variable charPtr and the assignment of its initial value could have been equivalently expressed in two separate statements, as follows:

```
char *charPtr;
charPtr = &c;
```

(and not by the statements)

```
char *charPtr;
*charPtr = &c;
```

as might be implied from the value of a pointer in Objective-C is meaningless until it is set to something.

The next NSLog call displays the contents of the variable c and the contents of the variable referenced by charPtr. Because you set charPtr to point to the variable c, the value displayed is the contents of c, as verified by the first line of your program output.

In the next line of the program, the character '/' is assigned to the variable c. Because charPtr still points to the variable c, displaying the value of *charPtr in the subsequent NSLog call correctly displays this new value of c at the terminal. Unless the value of charPtr changes, the expression *charPtr always accesses the value of c. Thus, as the value of c changes, so does the value of *charPtr.

The previous discussion can help you understand how the program statement that appears next in the program works. We mentioned that unless charPtr changed, the expression *charPtr = '(' would always reference the value of c. Therefore, in the expression

```
*charPtr = '(';
```

the parenthesis character being assigned to c. More, the character '(' is formally assigned to the variable charPtr points to. You know that this variable is c because you placed a pointer to c in charPtr at the beginning of the program.

The previous concepts are the key to your understanding of pointer operation. Review them at this point if they still seem a bit unclear.

# Pointers and Structures

You have seen how to define a pointer to point to a basic type such as an int or a char. But you can also define a pointer to point to a structure. Earlier in this chapter, you defined your date structure as follows:

```
struct date
{
  int month;
  int day;
  int year;
}
```
