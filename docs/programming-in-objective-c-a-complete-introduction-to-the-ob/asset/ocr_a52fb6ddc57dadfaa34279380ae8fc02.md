can add a main function to the preceding code to end up with a complete program, as shown in Program 13.3.

# Program 13.3

```
#import <Foundation/Foundation.h>

void printMessage(void)
{
    NSLog(\@Programming is fun.");
}

int main (int argc, char *argv[])
{
    AutoreleasePool *pool = [[AutoreleasePool alloc] init];

    printMessage();
    [pool drain];
    return 0;
}
```

# Program 13.3 Output

Programming is fun.

Program 13.3 consists of two functions: printMessage and main. As mentioned earlier, the idea of calling a function is not new. Because printMessage takes arguments, you call it simply by listing its name followed by a pair of open and close parentheses.

# Arguments and Local Variables

In Chapter 5, "Program Looping," you developed programs for calculating triangular number. Here you define a function to generate a triangular number and call it, appropriately enough, calculateTriangularNumber. As an argument to the function, you specify which triangular number to calculate. The function then calculates the desired number and displays the results. Program 13.4 shows the function to accomplish the task a main routine to try it.

# Program 13.4

```
#import <Foundation/Foundation.h>
```

```
// Function to calculate the nth triangular number

void calculateTriangularNumber(int n)
{
    int i, triangularNumber = 0;

    for (i = 1; i <= n; ++i)
        triangularNumber += i;

    NSLog (\@"Triangular number %d is %d", n, triangularNumber);
}
```