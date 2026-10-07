# Chapter 7 Functions: C++'s Programming Modules

Note
Some compilers require explicit instructions to search the math library. For example, older versions of g++ use this command line:

```
g++ structfun.C -lm
```

Here is a sample run of the program in Listing 7.12:

```
Enter the x and y values: 30 40
distance = 50, angle = 53.1301 degrees
Next two numbers (q to quit): -100 100
distance = 141.421, angle = 135 degrees
Next two numbers (q to quit): q
```

# Program Notes

We've already discussed the two functions in Listing 7.12, so let's review how the program use cin to control a loop:

Recall that cin is an object of the istream class. The extraction operator (>>) is designed in such a way that cin >> rplace.x is also an object of that type. As you'll see in Chapter 11, "Working with Classes," class operators are implemented with functions.
What happens when you use cin >> rplace.x is that the program calls a function that returns a typeream value. If you apply the extraction operator to the cin >> rplace.x object (as in cin >> rplace.x >> rplace.y), you again get an object of the istream class. Thus, the entire while loop test expression evaluates to cin, which, as you may recall, when used in the context of a test expression, is converted to a boolean value of true or false, depending on whatever input seeded. In the loop Listing 7.12, for example, cin expects to enter two numbers. If, the user enters q, as shown in the sample output, cin recognizes that q is not a number. It leaves the q in the input queue and returns a value that's converted to false, terminating the loop.

Compare that approach for reading numbers to this one:

To terminate this loop early, you enter a negative number. This restricts input to non-negative values. This restriction fits the needs of some programs, but more typically you