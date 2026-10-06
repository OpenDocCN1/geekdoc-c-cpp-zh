Somewhere you must have a routine called main, as we've previously noted. That's where your program always begins execution. Here's the program section from Program 3.2:

```
//--- program section -----
int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *myFraction;

        // Create an instance of a Fraction and initialize it

        myFraction = [Fraction alloc];
        myFraction = [myFraction init];

        // Set fraction to 1/3

        [myFraction setNumerator: 1];
        [myFraction setDenominator: 3];

        // Display the fraction using the print method
        NSLog("The value of myFraction is:");
        [myFraction print];
    }
    return 0;
}
```

Inside main, you define a variable called myFraction with the following line:

```
Fraction *myFraction;
```