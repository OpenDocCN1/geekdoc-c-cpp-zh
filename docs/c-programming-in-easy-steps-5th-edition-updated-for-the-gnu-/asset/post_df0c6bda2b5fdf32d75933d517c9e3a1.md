
![](img/db19f3858a1e321646bf2590afd29547_220_0.png)

The range of error code messages is implementation-defined. The range is larger on Linux systems than for the Windows platform.

## Getting the date and time

Current system time is usually counted as the number of seconds elapsed since the Epoch at 00:00:00 GMT on January 1, 1970. The total count represents the current date and time according to the Gregorian calendar and is referred to as “Calendar time”. Special functions to handle date and time are provided in the time.h header file along with a data type struct named tm in which to store date and time components, as below:

![](img/db19f3858a1e321646bf2590afd29547_221_0.png)

| Component | Description |
|-----------|-------------|
| int tm_sec | seconds after the minute, normally 0-59 |
| int tm_min | minutes after the hour, 0-59 |
| int tm_hour | hours since midnight, 0-23 |
| int tm_mday | day of the month, 1-31 |
| int tm_mon | months since January, 0-11 |
| int tm_year | years since 1900 |
| int tm_wday | days since Sunday, 0-6 |
| int tm_yday | days since January 1st, 0-365 |
| int tm_isdst | is Daylight Saving Time in effect |

The current elapsed seconds count is returned by a time(NULL) function as a time_t data type. This can then be specified as the argument to a localtime() function for conversion to its various tm struct components.

The struct components can be output in a standard date and time format using an asctime() function. Alternatively, individual components can be output using special time format specifiers with a strftime() function. This function requires four arguments to specify a char array in which to store the formatted date string, the maximum string length, the text and format specifiers to extract the required components, and the tm struct to be used.

![](img/db19f3858a1e321646bf2590afd29547_222_0.png)

The Daylight Saving component tm_isdst is positive if Daylight Saving is in effect; zero if not; or negative if that information is unavailable.

![](img/db19f3858a1e321646bf2590afd29547_222_1.png)

A complete list of all time format specifiers is included in the Reference section here.

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions and the date and time functions

```
#include <stdio.h>
#include <time.h>
```

![](img/db19f3858a1e321646bf2590afd29547_222_2.png)

datetime.c

- 2. Add a main function that declares a character array variable, a time_t variable, and a tm struct

```
int main()
{
    char buffer[100];
    time_t elapsed;
    struct tm *now;
}
```

Next, in the main function block, get the current elapsed seconds count since the Epoch

```
elapsed = time(NULL);
```

Now, convert the count to local time components

```
now = localtime( &elapsed );
```

Output the date and time in standard format

```
printf( "%s\n", asctime( now ) );
```

Then, output individual date and time components

```
strftime( buffer, 100, "Today is %A, %B %d.\n", now );
printf( "%s", buffer );
strftime( buffer, 100, "The time is %I:%M %p.\n", now );
printf( "%s", buffer );
```

Finally, return the required zero integer then save the program file; compile and execute the program to see the current date and time information

```
return 0;
```

![](img/db19f3858a1e321646bf2590afd29547_223_0.png)

![](img/db19f3858a1e321646bf2590afd29547_223_1.png)

Notice that the & addressof operator is used in the conversion to local time in order to get the Calendar time from the time_t data type.

## Running a timer

Getting the current time both before and after an event means that the duration of the event can be calculated by their difference. The **time.h** header file contains a **difftime()** function for that particular purpose. This function requires two arguments, both of which are of the **time_t** data type. It subtracts the second argument from the first argument and returns the difference expressed in whole seconds, but as a **double** data type.

Another way to work with time is offered by the **clock()** function from the **time.h** header file. This returns the processor time used since the program began, expressed in clock “ticks”. This function can be used to “pause” the execution of a program by running an empty loop until a future point in time is reached.

![](img/db19f3858a1e321646bf2590afd29547_224_0.png)

wait.c

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions and the date and time functions
```c
#include <stdio.h>
#include <time.h>
```
- 2. Next, declare a function prototype to pause the program
```c
void wait( int seconds );
```
- 3. Add a main function that declares two time_t variables, and an integer variable
```c
int main()
{
    time_t go , stop ;
    int i ;
}
```
- 4. Next, in the main function block, get the current time and output a message
```c
go = time( NULL );
```

```
printf ( "\nStarting countdown...\n\n" );
```

Add a loop to output a countdown value and call the other function on each iteration

```
for( i = 10 ; i > -1 ; i-- )
{
    printf ( " - %d", i );
    wait(1);
}
```

Next, in the main function block, get the current time once more then output the time taken to run the loop

```
stop = time( NULL );
printf("\nRuntime: %.0f seconds\n" , difftime( stop, go ) );
```

Finally, in the main function block, return a zero integer value, as required by the function declaration

```
return 0 ;
```

After the main function block, begin the function definition by initializing a clock_t variable at a future point beyond the current elapsed running time

```
void wait( int seconds )
{
    clock_t end_wait =
        ( clock() + ( seconds * CLOCKS_PER_SEC ));
}
```

Finally, in the wait function block, add an empty loop that terminates when the current time reaches the future point, returning control to the loop in the main function

```
while ( clock() < end_wait ) { }
```

Save the program file, then compile and execute the program to see the countdown timer and runtime

![](img/db19f3858a1e321646bf2590afd29547_225_0.png)

![](img/db19f3858a1e321646bf2590afd29547_226_0.png)

![](img/db19f3858a1e321646bf2590afd29547_226_1.png)

The number of clock ticks per second is implementation-dependent but is defined in time.h by the CLOCKS_PER_SEC constant.

![](img/db19f3858a1e321646bf2590afd29547_226_2.png)

You can find the elapsed runtime expressed in seconds by dividing the value returned by the clock() function by the CLOCKS_PER_SEC value.

## Generating random numbers

The `stdlib.h` header file provides a `rand()` function that generates a pseudo-random positive integer when called. This will, by default, return a number in the range from 0 to a large value (at least 32,767). A specific range can be set by using the modulus operator to specify a maximum upper limit – for example, to specify a range from 0 to 9 with the expression `rand() % 9`.

To set a minimum lower limit for the range, its value can be added to the result of the expression – for example, to specify a range from 1 to 10 with the expression `( rand() % 9 ) + 1`.

The numbers generated by the `rand()` function are not truly random, as the function successively generates the same sequence of numbers each time a program using `rand()` is executed. In order to generate a different sequence of numbers, the “seed” that starts the sequence must be specified. By default, the initial seed value is 1, but this can be changed by specifying an alternative integer argument to the `srand()` function – for example, `srand(8)`. This will cause `rand()` to generate a different sequence of numbers to those generated using the default seed value, but the sequence will still be repeated each time a program using `rand()` is executed.

To generate different random sequences upon successive execution the argument specified to `srand()` must be something other than a static integer. The common solution is to seed the `rand()` function with the current time in elapsed seconds with `srand( time( NULL ) )`.

Now, the sequence of numbers generated by `rand()` will be different each time a program using `rand()` is executed.

- 1. Begin a new program with preprocessor instructions to include the standard input/output library functions, random number, time, and string functions

```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>
```
