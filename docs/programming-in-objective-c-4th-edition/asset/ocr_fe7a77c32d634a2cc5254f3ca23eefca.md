Next, you create a mutable copy of dataArray and assign the resulting copy to dataArray2. This creates two distinct mutable arrays in memory, both containing three elements. Now when you remove the first element from dataArray2, it has no effect on the contents of dataArray, as verified by the last output for dataArray.

Note that making a mutable copy of an object does not require the object being copied be mutable. The same applies to immutable copies: You can make an immutable copy of a mutable object.

# Shallow Versus Deep Copying

Program 18.1 fills the elements of dataArray with immutable strings (recall that constant string objects are immutable). Program 18.2, you'll fill it with mutable strings instead so that you can change one of the strings in the array. Take a look at Program 18.2 and see whether you understand its output.

# Program 18.2

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSMutableArray *dataArray = [
            [NSMutableArray arrayWithObjects:
                [NSMutableString stringWithString:@"one"],
                [NSMutableString stringWithString:@"two"],
                [NSMutableString stringWithString:@"three\]]
        ];
    }
```