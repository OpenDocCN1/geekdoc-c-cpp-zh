```
NSLog (@"x = %i", x);
}
@end /////////////////////////
int main (int argc, char *argv[])n{
    autoreleasepool {
        ClassB *b = [[ClassB alloc] init];

        [b initVar]; // uses overriding method
        in B

        [b printVar]; // reveal value of x;
    }
    return 0;
}
```

# Program 8.6. Output

x = 200

Clearly, the message [b initVar]; causes the initVar method defined in ClassB to be used, and not the one defined in ClassA, as was the case with the previous example. Figure 8.9 illustrates this.

# Figure 8.9. Overriding the initVar method