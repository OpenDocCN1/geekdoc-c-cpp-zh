time the program executes. Once a program has been thoroughly debugged, it can be conditioned to produce a *different* sequence of random numbers for each execution. This is called **randomizing** and is accomplished with the C++ Standard Library function `srand` from the header `<cstdlib>`. Function `srand` takes an `unsigned` integer argument and **seeds** the `rand` function to produce a different sequence of random numbers for each execution.

# Demonstrating `srand`

**Figure 6.8** demonstrates function `srand`. The program produces a *different* sequence of random numbers each time it executes, provided that the user enters a *different seed*. We used the *same* seed in the first and third sample outputs, so the *same* series of 10 numbers is displayed in each of those outputs.

![](bbox=[0.121, 0.573, 0.194, 0.631])

# Software Engineering Observation 6.4

> *Ensure that your program seeds the random-number generator differently (and only once) each time the program executes; otherwise, an attacker would easily be able to determine the sequence of pseudorandom numbers that would be produced.*