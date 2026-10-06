initialized; the remaining values in the array are set to zero. Thus,
the declaration

```
float sample_data[500] = { 100.0, 300.0, 500.5
};
```

initializes the first three values of sample_data to 100.0, 300.0,
and 500.5 and sets the remaining 497 elements to 0.

By enclosing an element number in a pair of brackets, you can
initialize specific array elements in any order. For example,

```
int x = 1233;
int a[] = { [9] = x + 1, [2] = 3, [1] = 2, [0]
 = 1 };
```

defines a 10-element array called a (based on the highest index in
(the array) and initializes the last element to the value of x + 1
(1234). In addition, it initializes the first three elements to 1, 2, and
3, respectively.

# Character Arrays

Program 13.2 illustrates how you can use a character array.
However, one point is worthy of discussion. Can you spot it?

# Program 13.2

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[])
{
    @autoreleasepool {
        char word[] = { 'H', 'e', 'l', 'l', 'o',
        '!' };
```