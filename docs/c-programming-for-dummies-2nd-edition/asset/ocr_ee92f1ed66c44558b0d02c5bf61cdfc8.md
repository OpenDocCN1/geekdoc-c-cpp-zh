Also defined in the `time.h` header file are these chronological functions:

| Function | Description |
| --- | --- |
| *time()* | The *time()* function uses the address of the *time_t* variable as its argument. This function fills the *time_t* variable with the current Unix epoch time and it also returns a *time_t* value. |
| *ctime()* | The *ctime()* function consumes a *time_t* variable and converts it into a displayable date-time string. |
| *localtime()* | This function fills a *tm* structure with information based on the time value stored in a *time_t* variable. The *localtime()* function returns the address of the *tm* structure, so it gets all messy with structures and pointers and that `->` operator. |
| *difftime()* | The *difftime()* function compares the values between two *time_t* values and returns a *float* value as the difference in seconds. |

C libraries often come with other time-related functions, such as *sleep()* and *clock()*. These functions may not be available on all systems — which shouldn’t be a problem, because you can always code your own time functions.

# # Time to Program

I could imagine that the same Programming Lords who invented pointers and linked lists could really mess up your brain with time programming. Happily, they didn’t. Though a knowledge of pointers and structures helps you learn the ropes, time programming in C is straightforward.

# ## Checking the clock

The computer, or whichever device you’re programming, keeps a time value somewhere deep in its digital bosom. To access this value, you need to code a program that uses the *time()* function. It stuffs the current clock tick value into a *time_t* variable, as shown in Listing 21-1.