# Overriding Methods 169

Class Instance Variables Methods
Object
↓
ClassA x initVar
↓
ClassB x initVar printVar

![](bbox=[0.396, 0.248, 0.604, 0.28])

# Which Method Is Selected?

We covered how the system searches up the hierarchy for a method to apply to an object. If you have methods in different classes with the same name, the correct method is chosen based on the class of the receiver of the message. Program 8.7 uses the same class definition for ClassA and ClassB as before.

Program 8.7

```
#import <Foundation/Foundation.h>

// insert definitions for ClassA and ClassB here

int main (int argc, char *argv[]) {
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];
    ClassA *a [[ClassA alloc] init];
    ClassB *b [[ClassB alloc] init];

    [a initVar]; // uses ClassA method
    [a printVar]; // reveal value of x;

    [b initVar]; // use overriding ClassB method
    [b printVar]; // reveal value of x;
    [a release];
    [b release];

    [pool drain];
    return 0;
}
```

You'll get this warning message when you build this program:
warning: 'ClassA' may not respond to selector '-printVar'

What happened here? We talked about this in an earlier section. Take a look at the declaration for ClassA: