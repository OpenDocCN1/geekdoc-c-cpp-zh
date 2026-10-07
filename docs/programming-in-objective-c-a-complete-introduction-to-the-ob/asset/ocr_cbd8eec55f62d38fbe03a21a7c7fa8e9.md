defines a 10-element array called a (based on the highest index in the array) and initial-izes the element to the value of x + 1 (1234). In addition, it initializes the first three elements to 1, 2, and 3, respectively.

# Character Arrays

Program 13.2 illustrates how you can use a character array. However, one point is worthy of discussion. Can you spot it?

Program 13.2

```
#import <Foundation/Foundation.h>
int main (int argc, char *argv[]) {
    NSAutleasePool *pool = [NSAutleasePool alloc init];
    char word[] = { 'H', 'e', 'l', 'l', 'o', '!' };
    int i;

    for ( i = 0; i < 6; ++i ) {
        NSLog("@%c", word[i]);
    }
    [pool drain];
return 0;
}
```

Program 13.2 Output

H
e
l
l
o
!

In this case, the size of the array is determined automatically based on the number of initialization elements. Because Program 13.2 has six initial values listed for the array word, the Objective-C language implicitly dimensions the array to six elements.

This approach works fine as long as you initialize every element in the array at the point that the array is defined. If this is not to be the case, you must explicitly dimension the array.

If you put a terminating null ('\0') at the end of a character array, you create what is often called a character string. If you substitute the initialization of word in Program 13.2 with this

```
char word[] = { 'H', 'e', 'l', 'l', 'o', '!', '\0' };
```

you could have displayed the twenty string with a single NSLog call, like this:

```
NSLog("@%s", word);
```