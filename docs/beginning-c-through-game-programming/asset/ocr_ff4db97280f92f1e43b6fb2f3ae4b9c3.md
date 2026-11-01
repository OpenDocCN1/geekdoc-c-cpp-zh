seeding the random number generator. Game programmers give the random number generator a number, called a seed, to determine the starting place in this sequence of pseudorandom numbers.

The following code seeds the random number generator:

```
srand(static_cast<unsigned int>(time(0))); //seed random number generator
```

Wow, that's a pretty cryptic looking line, but what it does is simple. It seeds the random number generator based on the current date and time, which is perfect since the current date and time will be different for each run of the program.

In terms of the actual code, the srand() function seeds the random number generator—you just have to pass it an unsigned int as a seed. What gets passed to the function here is the return value of time(0)—a number based on the current system date and time. The code static_cast<unsigned int> just converts (or casts) this value to an unsigned int. Now, you don't have to understand all the nuances of this line; the least you need to know is that if you want a program to generate a series of random numbers that are different each time the program is run, your program should execute this line once before calls to rand().

> Hint
> 
> A comprehensive explanation of the various forms of casting a value from one type to another is beyond the scope of this book.

# Calculating a Number within a Range

After generating a random number, randomNumber holds a value between 0 and 32767 (based on my implementation of C++). But I need a number between 1 and 6, so next I use the modulus operator to produce a number in that range.

```
int die = (randomNumber % 6) + 1; // get a number between 1 and 6
```

Any positive number divided by 6 will give a remainder between 0 and 5. In the preceding code, I take this remainder and add 1, giving me the possible range of 1 through 6—exactly what I wanted. You can use this technique to convert a random number to a number within a range you're looking for.