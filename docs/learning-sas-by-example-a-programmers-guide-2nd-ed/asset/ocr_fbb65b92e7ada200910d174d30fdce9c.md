# Chapter 11: Working with Numeric Functions

Figure 11.6: Some of the Commonly Used Probability Distributions

| Distribution | Example | Description |
| --- | :--- | :--- |
| Uniform | X = rand('uniform'); | Uniform random numbers between 0 and 1 |
| Normal | HR = rand('normal',70,10); | Normally distributed numbers with a mean of 70 and a standard deviation of 10 |
| Bernoulli | Heads = rand('Bernoulli',5); | A Bernoulli distribution with p = .5 (simulates a coin toss) |
| Binomial | N = rand('Binomial',3,10) | The number of "successes" in 10 trials with a probability of _3 |

> Note: The RAND function replaces some of the older random number functions as RANUNI (generates uniform random numbers) and RANNOR (generates normally distributed random numbers).

You may wonder why you ever need to generate random numbers. Some uses are to create data sets for benchmarking, select random samples, and to assign subjects to two or more groups.

Computers do not really generate true random numbers. However, they are capable of generating series of numbers that are very close to random (called pseudo-random numbers by snobs). In order to get the computer started, you need to provide a seed number to generate the first number in the random sequence. If you use the RAND function without a seed with a call streaminit(n) command (where n is an integer, preferably a large one), SAS uses the computer's clock to supply the seed. If you choose any positive integer in the call streaminit, that number is used as a seed. SAS recommends you choose a seed of at least 7 digits. If you supply the seed, the program generates the same sequence of random numbers every time you run the program. Without the call to streaminit, the sequence changes every time you run the program. Hopefully, several examples will make this clear.

As the first example, you want to generate 5 uniform random numbers.

# Program 11.9: Program to Generate Five Uniform Random Numbers

```
data Uniform;
  do i = 1 to 5;
    x = rand('uniform');
    output;
  end;
run;
```

First, notice that this DATA step does not read any data. The DO loop causes the RAND function to execute 5 times and output 5 uniform random numbers. It is important that the OUTPUT statement is placed inside the loop, otherwise the program would only output one random number. Let's run this program once and list the output data set: