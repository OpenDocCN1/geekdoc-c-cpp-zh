# Just a Moment—Building a Time-Delay Loop

Sometimes it’s useful to build a time delay into a program. For example, you might have encountered programs that flash a message onscreen and then go on to something else before you can read the message. You end up being afraid that you’ve missed irretrievable information of vital importance. It would be much nicer if the program paused 5 seconds before moving on. The while loop is handy for producing this effect. A technique from the early days of personal computers was to make the computer count for a while to use up time:

```
long wait = 0;
while (wait < 10000)
    wait++;              // counting silently
```

The problem with this approach is that you have to change the counting limit when you change computer processor speed. Several games written for the original IBM PC, for example, became unmanageably fast when run on its faster successors. And these days a computer might even deduce that it can just set wait to 1000 and skip the loop. A better approach is to let the system clock do the timing for you.

The ANSI C and the C++ libraries have a function to help you do this. The function is called clock(), and it returns the system time elapsed since a program started execution. There are a couple complications, though. First, clock() doesn’t necessarily return the time in seconds. Second, the function’s return type might be long on some systems, unsigned long on others, and perhaps some other type on others.

But the ctime header file (time.h on less current implementations) provides solutions to these problems. First, it defines a symbolic constant, CLOCKS_PER_SEC, that equals the number of system time units per second. So dividing the system time by this value yields seconds. Or you can multiply seconds by CLOCKS_PER_SEC to get time in the system units. Second, ctime establishes clock_t as an alias for the clock() return type. (See the sidebar “Type Aliases,” later in this chapter.) This means you can declare a variable as type clock_t, and the compiler converts it to long or unsigned int or whatever is the proper type for your system.

Listing 5.14 shows how to use clock() and the ctime header to create a time-delay loop.

# Listing 5.14  `waiting.cpp`

```
// waiting.cpp -- using clock() in a time-delay loop
#include <ctime>
#include <ctime> // describes clock() function, clock_t type
int main()
{
    using namespace std;
    cout << "Enter the delay time, in seconds: ";
    float secs;
    cin >> secs;
    clock_t delay = secs * CLOCKS_PER_SEC;  // convert to clock ticks
```