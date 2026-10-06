Now it is time to show an actual program example that illustrates the use of the various bit operators (see Program 10.4).

# Program 10.4

```
// Bitwise operators illustrated
#import <Foundation/Foundation.h>
int main (int argc, char * argv[]) {
    @autoreleasepool {
        unsigned int w1 = 0xA0A0A0A0, w2 = 0xFFFF0000,
        w3 = 0x00007777;
        NSLog("@%x %x %x", w1 & w2, w1 | w2, ^ w2);
        NSLog("@%x %x %x", ~w1, ~w2, ~w3);
        NSLog("@%x %x %x", w1 ^ w1 & ~w2, w1 | w2 | ~w3);
        NSLog("@%x %x %x", w1 | w2 & w3, w1 | w2 & ~w3);
        NSLog ("@%x %x", ~(w1 & ~w2), ~(w1 | ~w2));
    }
    return 0;
}
```

# Program 10.4. Output