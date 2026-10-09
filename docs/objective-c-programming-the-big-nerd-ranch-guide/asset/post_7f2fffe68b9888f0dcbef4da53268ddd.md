
This block takes two doubles as arguments. A block can have a return value as well, but we'll come back to that.

Do these blocks have names? Not yet. These blocks are values, like the number 5 is a value. To be able to access a block by a name, we have to assign it to a *block variable*.

## Using blocks

To see how this works, we're going to dive right into some code. In this exercise, you're going to use a block to remove all of the vowels from each of the strings in an array.

Create a new Foundation Command Line Tool and call it VowelMovement. In this program, you will use a block to iterate over an array of strings, transforming each one. First, you're going to create three arrays: one to store the original strings, one to store the “devowelized” strings, and a third to store the characters to strip from the strings. In main.m, replace the code inside of the @autoreleasepool's curly braces:

```objective-c
int main (int argc, const char * argv[]) 
{
    @autoreleasepool {
        
        // Create the array of strings to devowelize and a container for new ones
        NSArray *oldStrings = [NSArray arrayWithObjects:
                               @"Sauerkraut", @"Raygun", @"Big Nerd Ranch", @"Mississippi", nil];
        NSLog(@"Old strings: %@", oldStrings);
        NSMutableArray *newStrings = [NSMutableArray array];
        
        // Create a list of characters that we'll remove from the string
        NSArray *vowels = [NSArray arrayWithObjects:
                           @"a", @"e", @"i", @"o", @"u", nil];
    }
    return 0;
}
```

Nothing new here; you're just setting up arrays. Build and run your program. You can ignore the warnings about unused variables for now.

## Declaring a block variable

Now comes the code for the block. Although blocks look like functions, they can be stored in variables. Like other variables, block variables are declared and then assigned values. Add the following code to main.m to declare your block variable.

```objective-c
int main (int argc, const char * argv[]) 
{
    @autoreleasepool {
        
        // Create the array of strings to devowelize and a container for new ones
        NSArray *oldStrings = [NSArray arrayWithObjects:
                               @"Sauerkraut", @"Raygun", @"Big Nerd Ranch", @"Mississippi", nil];
        NSLog(@"Old strings: %@", oldStrings);
        NSMutableArray *newStrings = [NSMutableArray array];
        
        // Create a list of characters that we'll remove from the string
        NSArray *vowels = [NSArray arrayWithObjects:
                           @"a", @"e", @"i", @"o", @"u", nil];

        // Declare the block variable
        void (^devowelizer)(id, NSUInteger, BOOL *);
    }
    return 0;
}
```

Let's break down this declaration to see what's going on.

### Figure 32.1  Block variable declaration

![](img/5f9368899ebf8d92fc145f8def1e89f8_239_0.png)

When declaring a primitive variable, you give its type and then its name, like `int i`. For a block variable, however, the name is in the middle of the declaration right after the caret. The type of the block variable is dependent on how the block is constructed. In this case, `devowelizer`'s type is “a block that takes an object, an integer, and a BOOL pointer, and returns nothing.”

## Assigning a block

Now let's assign a value to our new variable. For a block variable, the value is always a set of instructions inside curly braces. In main.m, add the following assignment:

```objective-c
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        // Create the array of strings to devowelize and a container for new ones
        NSArray *oldStrings = [NSArray arrayWithObjects:
        @"Sauerkraut", @"Raygun", @"Big Nerd Ranch", @"Mississippi", nil];
        NSLog(@"old strings: %@", oldStrings);
        NSMutableArray *newStrings = [NSMutableArray array];
        
        // Create a list of characters that we'll remove from the string
        NSArray *vowels = [NSArray arrayWithObjects:
        @"a", @"e", @"i", @"o", @"u", nil];
        
        // Declare the block variable
        void (^devowelizer)(id, NSUInteger, BOOL *);

        // Assign a block to the variable
        devowelizer = ^(id string, NSUInteger i, BOOL *stop) {

            NSMutableString *newString = [NSMutableString stringWithString:string];

            // Iterate over the array of vowels, replacing occurrences of each
            // with an empty string.
            for (NSString *s in vowels) {
                NSRange fullRange = NSMakeRange(0, [newString length]);
                [newString replaceOccurrencesOfString:s
                                       withString:@""
                                         options:NSCaseInsensitiveSearch
                                           range:fullRange];
            }

            [newStrings addObject:newString];
        }; // End of block assignment
    }
    return 0;
}
```

Build your program again to check your typing. The warnings about unused variables should disappear. Now you’ve composed a block – a set of instructions – and assigned the block to the block variable `devowelizer`. Notice that the block assignment ends with a semi-colon just like any variable assignment would.

As with any variable, you can perform the declaration and assignment of `devowelizer` together:

```objective-c
void (^devowelizer)(id, NSUInteger, BOOL *) = ^(id string, NSUInteger i, BOOL *stop) {

    NSMutableString *newString = [NSMutableString stringWithString:string];

    // Iterate over the array of vowels, replacing occurrences of each
    // with an empty string.
    for (NSString *s in vowels) {
        NSRange fullRange = NSMakeRange(0, [newString length]);
        [newString replaceOccurrencesOfString:s
                                       withString:@""
                                         options:NSCaseInsensitiveSearch
                                           range:fullRange];
    }

    [newStrings addObject:newString];
};
```

Just like before, here we declare a block variable that takes three arguments, returns nothing, and is called `devowelizer`. Then we compose an actual block and store it in `devowelizer`.

## Passing in a block

Because `devowelizer` is a variable, you can pass it as an argument. **NSArray** has a method called **enumerateObjectsUsingBlock:**. This method expects a block as its sole argument. It will execute that block once for each object in the array.

In main.m, add the following code to call **enumerateObjectsUsingBlock:** with `devowelizer` and then print out the devoweIized strings.

```objective-c
int main (int argc, const char * argv[]) {
    @autoreleasepool {
        // Create the array of strings to devowelize and a container for new ones
        NSArray *oldStrings = [NSArray arrayWithObjects:
                             @"Sauerkraut", @"Raygun", @"Big Nerd Ranch", @"Mississippi", nil];
        NSLog(@"old strings: %@", oldStrings);
        NSMutableArray *newStrings = [NSMutableArray array];
        
        // Create a list of characters that we'll remove from the string
        NSArray *vowels = [NSArray arrayWithObjects:
                          @"a", @"e", @"i", @"o", @"u", nil];
        
        // Declare the block variable
        void (^devowelizer)(id, NSUInteger, BOOL *);
        
        // Assign a block to the variable
        devowelizer = ^(id string, NSUInteger i, BOOL *stop) {
            NSMutableString *newString = [NSMutableString stringWithString:string];
            
            // Iterate over the array of vowels, replacing occurrences of each
            // with an empty string.
            for (NSString *s in vowels) {
                NSRange fullRange = NSMakeRange(0, [newString length]);
                [newString replaceOccurrencesOfString:s
                                           withString:@""
                                             options:NSCaseInsensitiveSearch
                                               range:fullRange];
            }
            
            [newStrings addObject:newString];
        } ; // End of block assignment
        
        // Iterate over the array with our block
        [oldStrings enumerateObjectsUsingBlock:devowelizer];
        NSLog(@"new strings: %@", newStrings);
    }
    return 0;
}
```

Build and run your program. You’ll see two arrays logged to the console. The second array should match the first array – without all those pesky vowels.

```
2011-09-03 10:27:02.617 VowelMovement[787:707] old strings: (
    Sauerkraut,
    Raygun,
    "Big Nerd Ranch",
    Mississippi
)
```
