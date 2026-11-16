
## Variable Length Argument List: Advanced

It is possible to create functions that receive an unspecified number of arguments! In fact, printf() takes a variable number of arguments. As a minimum, printf() must receive a string as its first argument, but can receive any number of additional arguments. The actual function prototype for printf() is:

```
int printf(char *fmt, ...);
```

The declaration ... (ellipsis) means that the number and types of these arguments may vary. The function may receive a variable number of arguments of any type. This declaration can only appear at the end of an argument list.

Declaring a function with a variable number of arguments can provide us great flexibility. Consider a function average() that can find the average of a variable number of arguments. It might be invoked as follows:

```
avg = average(a, b, c);
avg = average(a, b, c, d);
```

The secret to handling a variable number of arguments in C lies in the way arguments are passed to a function. Let's take a look at the contents of the stack at the moment a C function is entered. When a function is called, the arguments followed by the return address are placed on the stack:

```
foo(arg1, arg2);

high addresses
---------------
    arg2
---------------
    arg1
---------------
sp--> return address
---------------
    stack
    grows
    downward
---------------
low addresses
```

In C, the arguments of the functions are placed on the stack in the reverse order they appear in the function call. The result is that the first argument is always at a fixed offset from the stack pointer, sp. The offset is the number of bytes needed to store the return address. So no matter how many arguments are passed to a C function, the first argument is always easily reachable.

So upon entry to the C function, the first argument appears on the stack just above the return address, i.e., it has the next higher address. Additional arguments have successively higher addresses. Therefore, if you could get to the first argument on the stack and you know the size of all the other arguments, you could then retrieve the arguments one by one!

There is a standard C header file, stdarg.h, that contains a set of macros along with a newly defined data type that makes the task of handling a variable number of arguments straightforward. The implementation of this header file will vary from machine to machine, but the interface it presents is uniform. The first thing that stdarg.h contains is the definition of a new data type:

```
va_list
```

that is used to declare a variable that will refer to each argument in turn:

```
va_list ap;
```

We declare ap to be an argument pointer of type va_list. ap will be used by the other macros to process the variable-length argument list, i.e., ap will point to each argument in turn.

va_start is a macro which initializes the argument pointer, ap, to point to the first unnamed argument on the stack being passed to the function. va_start must be called once before ap is used to access any of the unnamed arguments. The prototype for va_start is:

```
void va_start(va_list ap, lastarg);
```

The first argument, ap, is the argument pointer. The second argument, lastarg, is the name of the rightmost fixed function parameter being passed to the called function. This is the rightmost argument in the argument list before the ellipsis (...). Note that there must be at least one named argument to the function. va_arg is a macro that advances the argument pointer, ap, to the next argument on the stack. The first time va_arg is used, it returns the first argument in the list. Each successive time va_arg is used, it returns the next argument in the list. It does this by first dereferencing ap, and then incrementing ap to point to the following item.

The prototype for va_arg is:

```
type va_arg(va_list ap, type);
```

The first argument, ap, is the argument pointer. The second argument, type, represents the type of the value expected in the argument list such as int, double, etc. Note that we can't use char, unsigned char, or float. va_arg uses the type name to both perform the dereference to determine what type to return and to determine how big a step to take to locate the next argument on the stack. The macro returns the value of the argument type.

va_end is a macro which does whatever cleanup is necessary to help the called function perform a normal return. It must be called after va_arg has read all of the arguments and before the function returns. Failure to do so might cause strange, undefined behavior in your program. va_end is prototyped as follows:

```
void va_end(va_list ap);
```

The argument, ap, is the argument pointer.

The following program returns the average of a series of numbers. The first argument of the function average() is always the number of values to be averaged:

```
// arg1.c

#include <stdio.h>
#include <stdarg.h>

int main(void);
double average(int num, ...);

int main(void) {
    double a = 2.0, b = 4.0, c = 6.0, d = 8.0;

    printf("%.1f\n", average(2, a, b));
    printf("%.1f\n", average(3, a, b, c));
    printf("%.1f\n", average(4, a, b, c, d));
    return 0;
}

double average(int num, ...) {
    int i;

    double total = 0.0;
    va_list ap;

    va_start(ap, num);
    for(i = 1; i <= num; i++) {
        total += va_arg(ap, double);
    }
    va_end(ap);
    return total / num;
}
```

The following program calculates the sum of a zero terminated list:

```
// arg2.c

#include <stdio.h>
#include <stdarg.h>

int main(void);
void sum(char *msg, ...);

int main(void) {
    sum("The total of 1+2+3+4 is %d\n", 1,2,3,4,0);
}

void sum(char *msg, ...) {
    int total = 0, arg;
    va_list ap;

    va_start(ap, msg);
    while ((arg = va_arg(ap,int)) != 0) {
        total += arg;
    }
    printf(msg, total);
    va_end(ap);
}
```

Finally, how does `printf()` and `scanf()` know what type to use in each `va_arg` macro? The answer is that they scan the format conversion specifiers in the format control string to determine the type of the next argument to be processed. Kernighan and Ritchie give an implementation of a minimal version of `printf()` to show how to write a function that processes a variable-length argument list. Its prototype is:

```
void myprintf(char *fmt, ...);
```

Since the interest here is in argument passing, `myprintf()` processes the format string and arguments but calls the real `printf()` function to do the format conversions:

```
// arg3.c

#include <stdio.h>
#include <stdarg.h>

int main(void);
void myprintf(char *fmt, ...);

int main(void) {
    int x = 5, y = 10;
    float pi = 3.14;
    char *buf = "Hello";

    myprintf("%d %d\n", x, y);
    myprintf("%d %f %s %d\n", x, pi, buf, y);
}

void myprintf(char *fmt, ...) {
    char *p, *sval;
    int ival;
    double dval;
    va_list ap;

    va_start(ap, fmt);
    for(p = fmt; *p; p++) {
        if (*p != '%') {
            putchar(*p);
            continue;
        }
        switch(*++p) {
            case 'd': ival = va_arg(ap, int);
                printf("%d", ival);
                break;
            case 'f': dval = va_arg(ap, double);
                printf("%f", dval);
                break;
            case 's':
                for(sval = va_arg(ap, char *); *sval; sval++)
                    putchar(*sval);
                break;
            default : putchar(*p);
                break;
        }
    }
    va_end(ap);
}
```

## Data Compression - Advanced

Data compression is the technique of reducing the number of bits needed to store or transmit data. Compression can be either lossless or lossy. Lossless and lossy compression are terms that describe whether or not all original data can be recovered when a file is uncompressed or a data transmission is received.

With lossless compression, every single bit of data that was originally in the file remains after the file is uncompressed. All of the information is completely restored. This is generally the technique of choice for text or spreadsheet files, where losing words or financial data could pose a problem. The Graphics Interchange File (GIF) is an image format used on the Web that provides lossless compression. Additional lossless compression algorithms are:

- TIFF - Zip - RAR - FLAC - LZW - Huffman Code - PNG - Morse Code

On the other hand, lossy compression reduces a file by permanently eliminating certain information, especially redundant information. When the file is uncompressed, only a part of the original information is still there (although the user may not notice it). Lossy compression is generally used for video and audio, where a certain amount of information loss will not be detected by most users. The JPEG image file, commonly used for photographs and other complex still images on the web, is an image that has lossy compression. Using JPEG compression, the creator can decide how much loss to introduce and make a trade-off between file size and image quality. Additional lossy compression algorithms are:

- MP3 - JPG - DivX

## Dictionary Compression

By examining the relationships between successive data items in a dictionary, one can derive an efficient coding scheme to achieve a high level of data compression. The compression technique takes advantage of the fact that words in a dictionary, being in alphabetical order, tend to start with the same letters as their neighboring entries. The compression algorithm works as follows: each word in the compressed dictionary starts with a digit that indicates how many characters should be copied from the preceding word in the dictionary. The rest of the letters for the word follow the digit.
