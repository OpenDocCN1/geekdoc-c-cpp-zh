
If the generated point lies inside the circle, we count it as a *hit*. That is the case when $x^2 + y^2 \le 1$. Because our shots are entirely random, we expect that the ratio of *hits* / *tries* is approximately equal to the ratio of the areas of the circle and the square, that is, $\pi / 4$. Therefore, our estimate for $\pi$ is $4 \times \text{hits} / \text{tries}$. This method yields an estimate for $\pi$, using nothing but simple arithmetic.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_198_0.png)

To run the Monte Carlo simulation, you have to work a little harder with random number generation. When you throw a die, it has to come up with one of six faces. When throwing a dart, however, there are many possible outcomes. You must generate a random floating-point value.

First, generate the following value:

```cpp
double r = rand() * 1.0 / RAND_MAX; // Between 0 and 1
```

The value `r` is a random floating-point value between 0 and 1. (You have to multiply by 1.0 to ensure that one of the operands of the `/` operator is a floating-point number.) The division `rand() / RAND_MAX` would be an integer division—see Common Error 2.3.

To generate a random value between −1 and 1, you compute:

```cpp
double x = -1 + 2 * r; // Between −1 and 1
```

As `r` ranges from 0 to 1, `x` ranges from −1 + 2 × 0 = −1 to −1 + 2 × 1 = 1.

Here is the program that carries out the simulation.

### ch04/montecarlo.cpp

```cpp
#include <iostream>
#include <cstdlib>
#include <cmath>
#include <ctime>

using namespace std;

int main()
{
    const int TRIES = 10000;

    srand(time(0));

    int hits = 0;
    for (int i = 1; i <= TRIES; i++)
    {
        double r = rand() * 1.0 / RAND_MAX; // Between 0 and 1
        double x = -1 + 2 * r; // Between −1 and 1
        r = rand() * 1.0 / RAND_MAX;
        double y = -1 + 2 * r;
        if (x * x + y * y <= 1) { hits++; }
    }
    double pi_estimate = 4.0 * hits / TRIES;
    cout << "Estimate for pi: " << pi_estimate << endl;
    return 0;
}
```

### Program Run

```text
Estimate for pi: 3.1504
```

- 43. How do you simulate a coin toss with the `rand` function?
- 44. How do you simulate the picking of a random playing card?
- 45. Why does the `dice.cpp` file include the `<ctime>` header?
- 46. In many games, you throw a pair of dice to get a value between 2 and 12. What is wrong with this simulated throw of a pair of dice?

  ```cpp
  int sum = rand() % 11 + 2;
  ```

- 47. How do you generate a random floating-point number between 0 and 100?

## Practice It

Now you can try these exercises at the end of the chapter: R4.24, P4.10, P4.25.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_199_0.png)

## *Random Fact 4.2* Software Piracy

As you read this, you have written a few computer programs, and you have experienced firsthand how much effort it takes to write even the humblest of programs. Writing a real software product, such as a financial application or a computer game, takes a lot of time and money. Few people, and fewer companies, are going to spend that kind of time and money if they don’t have a reasonable chance to make more money from their effort. (Actually, some companies give away their software in the hope that users will upgrade to more elaborate paid versions or pay for consulting. Other companies give away the software that enables users to read and use files but sell the software needed to create those files. Finally, there are individuals who donate their time, out of enthusiasm, and produce programs that you can copy freely. See Random Fact 9.2 for more information.)

When selling software, a company must rely on the honesty of its customers. It is an easy matter for an unscrupulous person to make copies of computer programs without paying for them. In most countries that is illegal. Most governments provide legal protection, such as copyright laws and patents, to encourage the development of new products. Countries that tolerate widespread piracy have found that they have an ample cheap supply of foreign software, but no local manufacturers willing to design good software for their own citizens, such as word processors in the local script or financial programs adapted to the local tax laws.

When a mass market for software first appeared, vendors were enraged by the money they lost through piracy. They tried to fight back by various schemes to ensure that only the legitimate owner could use the software, such as dongles—devices that must be attached to a printer port before the software will run. Legitimate users hated these measures. They paid for the software, but they had to suffer through inconveniences, such as having multiple dongles stick out from their computer. In the United States, market pressures forced most vendors to give up on these copy protection schemes, but they are still commonplace in other parts of the world.

Because it is so easy and inexpensive to pirate software, and the chance of being found out is minimal, you have to make a moral choice for yourself. If a package that you would really like to have is too expensive for your budget, do you steal it, or do you stay honest and get by with a more affordable product?

Of course, piracy is not limited to software. The same issues arise for other digital products as well. You may have had the opportunity to obtain copies of songs or movies without payment. Or you may have been frustrated by a copy protection device on your music player that made it difficult for you to listen to songs that you paid for. Admittedly, it can be difficult to have a lot of sympathy for a musical ensemble whose publisher charges a lot of money for what seems to have been very little effort on their part, at least when compared to the effort that goes into designing and implementing a software package. Nevertheless, it seems only fair that artists and authors receive some compensation for their efforts. How to pay artists, authors, and programmers fairly, without burdening honest customers, is an unsolved problem at the time of this writing, and many computer scientists are engaged in research in this area.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_199_1.png)

## CHAPTER SUMMARY

### Explain the flow of execution in a loop.

- Loops execute a block of code repeatedly while a condition remains true.
- An off-by-one error is a common error when programming loops. Think through simple test cases to avoid this type of error.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_200_0.png)

### Use the technique of hand-tracing to analyze the behavior of a program.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_200_1.png)

- Hand-tracing is a simulation of code execution in which you step through instructions and track the values of the variables.
- Hand-tracing can help you understand how an unfamiliar algorithm works.
- Hand-tracing can show errors in code or pseudocode.

### Use `for` loops for implementing counting loops.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_200_2.png)

- The `for` loop is used when a value runs from a starting point to an ending point with a constant increment or decrement.

### Choose between the `while` loop and the `do` loop.

- The `do` loop is appropriate when the loop body must be executed at least once.

### Implement loops that read sequences of input data.

- A sentinel value denotes the end of a data set, but it is not part of the data.
- You can use a Boolean variable to control a loop. Set the variable to true before entering the loop, then set it to false to leave the loop.
- Use input redirection to read input from a file. Use output redirection to capture program output in a file.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_200_3.png)

### Use the technique of storyboarding for planning user interactions.

- A storyboard consists of annotated sketches for each step in an action sequence.
- Developing a storyboard helps you understand the inputs and outputs that are required for a program.
